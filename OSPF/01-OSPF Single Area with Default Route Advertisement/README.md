# OSPF Single Area with Default Route Advertisement

## Objective

Configure Single Area OSPF to dynamically exchange routing information between routers within Area 0 and verify end-to-end connectivity.

---

## Topology

![Topology](topology.png)

---

## How it Works

In this lab, Single Area OSPF was configured to dynamically exchange routing information between multiple routers. First, IP addresses were manually assigned to all router interfaces and loopback interfaces. OSPF was then configured by advertising the required networks into Area 0 using network statements. Passive interfaces were configured on loopback interfaces to prevent unnecessary OSPF neighbor formation while still advertising the networks. A default static route was also configured and advertised into OSPF using the `default-information originate` command. Finally, neighbor relationships, the OSPF database, routing table, and end-to-end connectivity were verified.

---

## Verification

### OSPF Neighbors

Verified that OSPF neighbor relationships were successfully established using:

- `show ip ospf neighbor`

### OSPF Database

Verified the learned LSAs using:

- `show ip ospf database`

### Routing Table

Verified dynamically learned OSPF routes using:

- `show ip route`

### OSPF Information

Verified Router ID and OSPF process information using:

- `show ip ospf`
- `show ip protocols`

### Connectivity Test

Verified successful communication between end devices using ping.

---

## Skills Learned

- Single Area OSPF
- OSPF Neighbor Formation
- Passive Interfaces
- Loopback Interfaces
- Automatic Router ID Selection
- Default Route Advertisement
- OSPF Database Verification
- Routing Table Verification

---

## Devices Used

- 4 × Cisco 2691 Routers
- 1 × ISP Router
- 1 × Ethernet Switch
- 1 × VPCS Host

---

## Files Included

- `OSPF Single Area with Default Route Advertisement.gns3`
- `R1-config.txt`
- `R2-config.txt`
- `R3-config.txt`
- `R4-config.txt`
- `R5-config.txt`
- `PC1-config.txt`
- `R1-config.png`
- `R2-config.png`
- `R3-config.png`
- `R4-config.png`
- `R5-config.png`
- `PC1-config.png`