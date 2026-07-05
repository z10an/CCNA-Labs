# OSPF Cost Manipulation Lab

## Objective

Manually modify OSPF interface costs to influence path selection between multiple available routes.

---

## Topology

![Topology](topology.png)

---

## How it Works

In this lab, equal-cost paths existed between the source and destination networks. The OSPF cost of one interface was manually increased using the `ip ospf cost` command. OSPF recalculated the shortest path and selected the lower-cost route as the preferred path. This demonstrates how network administrators can influence traffic flow by adjusting interface metrics without changing the physical topology.

---

## Verification

### Interface Cost

Verified the manually configured interface cost using:

- `show ip ospf interface`

### Routing Table

Verified that OSPF selected the preferred path using:

- `show ip route`

### Connectivity Test

Verified successful communication between end devices using ping.

---

## Skills Learned

- Manual OSPF Cost Configuration
- Path Selection
- OSPF Metric Manipulation
- Routing Table Verification

---

## Devices Used

- 4 × Cisco 2691 Routers
- 1 × ISP Router
- 1 × Ethernet Switch
- 1 × VPCS Host

---

## Files Included

- `OSPF Cost Manipulation.gns3`
- `R1-config.txt`
- `PC1-config.txt`
- `R1-config.png`
- `PC1-config.png`
- `topology.png`