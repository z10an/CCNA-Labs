# GLBP (Gateway Load Balancing Protocol) Lab

## Objective

Configure Gateway Load Balancing Protocol (GLBP) to provide both default gateway redundancy and load balancing across multiple routers. Verify Active Virtual Gateway (AVG) election, Active Virtual Forwarder (AVF) operation, failover, and automatic recovery.

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

The following GLBP configuration was implemented:

- Three routers participate in each GLBP group.
- The router with the highest priority becomes the Active Virtual Gateway (AVG).
- Remaining routers become Active Virtual Forwarders (AVFs).
- Hosts use a single Virtual IP as their default gateway.
- Multiple routers simultaneously forward traffic using different Virtual MAC addresses.
- Automatic failover occurs if an AVG or AVF fails.
- Preemption allows the preferred router to automatically regain the AVG role.

---

## How it Works

Gateway Load Balancing Protocol (GLBP) is a Cisco First Hop Redundancy Protocol (FHRP) that provides both gateway redundancy and load balancing.

Unlike HSRP and VRRP, which allow only one router to actively forward traffic, GLBP distributes traffic across multiple routers. A single router is elected as the Active Virtual Gateway (AVG), which answers ARP requests for the Virtual IP address.

Instead of always returning the same Virtual MAC address, the AVG assigns different Virtual MAC addresses to different hosts. Each Virtual MAC belongs to an Active Virtual Forwarder (AVF), allowing multiple routers to forward traffic simultaneously.

If an AVG or AVF fails, another participating router automatically assumes its responsibilities, ensuring uninterrupted connectivity.

---

## Verification

### GLBP Status

Verified GLBP operation using:

- `show glbp`
- `show glbp brief`

### Interface Verification

Verified interface status using:

- `show ip interface brief`

### Configuration Verification

Verified GLBP configuration using:

- `show running-config`

### Connectivity Testing

Verified gateway redundancy and forwarding using:

- `ping`

---

## Key Concepts Learned

- Gateway Load Balancing Protocol (GLBP)
- First Hop Redundancy Protocol (FHRP)
- Active Virtual Gateway (AVG)
- Active Virtual Forwarder (AVF)
- Virtual IP Address
- Virtual MAC Address
- Load Balancing
- Gateway Redundancy
- GLBP Priority
- Preemption

---

## Engineering Observations

This lab demonstrated several important GLBP concepts:

- Multiple routers can simultaneously forward user traffic.
- A single Virtual IP is shared by all participating routers.
- Different hosts may receive different Virtual MAC addresses during ARP resolution.
- Each Virtual MAC is owned by an Active Virtual Forwarder (AVF).
- The Active Virtual Gateway (AVG) manages ARP requests and assigns Virtual MAC addresses.
- If an AVF fails, another router automatically assumes ownership of its Virtual MAC.
- GLBP provides both redundancy and efficient utilization of multiple routers.

---

## Troubleshooting Experience

During implementation and testing, the following tasks were performed:

- Verified all routers belonged to the same GLBP group.
- Confirmed Virtual IP consistency across all participating routers.
- Verified AVG and AVF elections using GLBP show commands.
- Observed multiple Active Virtual Forwarders operating simultaneously.
- Tested failover by shutting down the Active Virtual Gateway interface.
- Verified automatic recovery after restoring the failed router.
- Confirmed uninterrupted host connectivity during failover.

---

## Skills Learned

- GLBP Configuration
- Gateway Redundancy
- Gateway Load Balancing
- AVG and AVF Election
- Virtual MAC Operation
- Failover Testing
- High Availability Configuration
- Enterprise Gateway Design

---

## Devices Used

- 3 × Cisco Routers
- 2 × Ethernet Switches
- 2 × VPCS Hosts

---

## Files Included

- `glbp-lab.gns3`
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