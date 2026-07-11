# HSRP (Hot Standby Router Protocol) Lab

## Objective

Configure Hot Standby Router Protocol (HSRP) to provide highly available default gateway redundancy across two LANs. Verify Active/Standby election, Virtual IP operation, failover, and automatic recovery using preemption.

---

## Topology

![Topology](topology.png)

---

## Network Addressing

### Left LAN

| Device | IP Address |
|---------|------------|
| PC1 | 192.168.10.10/24 |
| R1 Fa0/0 | 192.168.10.1 |
| R2 Fa0/0 | 192.168.10.2 |
| R3 Fa0/0 | 192.168.10.3 |
| **Virtual Gateway** | **192.168.10.5** |

### Right LAN

| Device | IP Address |
|---------|------------|
| PC2 | 192.168.20.10/24 |
| R1 Fa0/1 | 192.168.20.1 |
| R2 Fa0/1 | 192.168.20.2 |
| R3 Fa0/1 | 192.168.20.3 |
| **Virtual Gateway** | **192.168.20.5** |

---

## Network Policies

The following HSRP configuration was implemented:

- Three routers participate in each HSRP group.
- The router with the highest priority becomes the Active router.
- The router with the second-highest priority becomes the Standby router.
- Remaining routers remain in the Listen state.
- Hosts use the Virtual IP as their default gateway.
- Automatic failover occurs if the Active router becomes unavailable.
- Preemption allows the highest-priority router to automatically reclaim the Active role after recovery.

---

## How it Works

HSRP is a Cisco First Hop Redundancy Protocol (FHRP) that provides gateway redundancy by creating a Virtual IP address shared among multiple routers.

Instead of configuring a physical router as the default gateway, hosts use the Virtual IP address. The participating routers exchange Hello packets to determine which router should become the Active router.

The Active router owns the Virtual IP and Virtual MAC address and forwards all host traffic. The Standby router continuously monitors the Active router through Hello messages and immediately assumes the Active role if the current Active router fails.

Additional routers remain in the Listen state, participating in HSRP but waiting until they are needed.

Because preemption is enabled, when a higher-priority router returns to service, it automatically resumes the Active role.

---

## Verification

### HSRP Status

Verified HSRP operation using:

- `show standby`
- `show standby brief`

### Interface Verification

Verified interface status using:

- `show ip interface brief`

### Configuration Verification

Verified HSRP configuration using:

- `show running-config`

### Connectivity Testing

Verified successful gateway failover using:

- `ping`

---

## Key Concepts Learned

- Hot Standby Router Protocol (HSRP)
- First Hop Redundancy Protocol (FHRP)
- Active Router
- Standby Router
- Listen State
- Virtual IP Address
- Virtual MAC Address
- HSRP Priority
- Preemption
- Hello Packets
- Gateway Redundancy

---

## Engineering Observations

This lab demonstrated several important HSRP concepts:

- Hosts always use the Virtual IP as their default gateway.
- The Virtual MAC address remains constant during router failover.
- Router priority determines Active and Standby election.
- Multiple routers can participate in a single HSRP group.
- Only one router forwards traffic at any given time.
- Preemption ensures the preferred router automatically resumes the Active role after recovering.
- Gateway redundancy minimizes network downtime without requiring host configuration changes.

---

## Troubleshooting Experience

During implementation and testing, the following tasks were performed:

- Verified all routers were participating in the correct HSRP groups.
- Confirmed matching Virtual IP addresses across participating routers.
- Verified Active, Standby, and Listen state elections.
- Tested failover by shutting down the Active router interface.
- Verified automatic Active router recovery after enabling the interface.
- Confirmed uninterrupted host connectivity using the Virtual Gateway.

---

## Skills Learned

- HSRP Configuration
- Gateway Redundancy
- First Hop Redundancy Protocols
- Active/Standby Election
- Failover Testing
- High Availability Configuration
- Enterprise Gateway Design
- Network Resiliency

---

## Devices Used

- 3 × Cisco Routers
- 2 × Ethernet Switches
- 2 × VPCS Hosts

---

## Files Included

- `hsrp-basic-lab.gns3`
- `R1-config.txt`
- `R2-config.txt`
- `R3-config.txt`
- `PC1-config.txt`
- `PC2-config.txt`
- `R1-config.png`
- `R2-config.png`
- `R3-config.png`
- `PC1-config.png`
- `PC2-config.png`
- `topology.png`