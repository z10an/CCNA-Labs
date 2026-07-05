# RIP Passive Interface Lab

## Objective

Configure a passive interface in RIP version 2 to prevent routing updates from being sent through specific interfaces while continuing to advertise the connected network to neighboring routers.

---

## Topology

![Topology](topology.png)

---

## How it Works

In this lab, I configured RIP version 2 and enabled the `passive-interface` feature on the LAN interfaces connected to the PCs. First, I manually configured the IP addresses of all PCs and router interfaces. Then, I enabled RIP version 2, disabled automatic route summarization using `no auto-summary`, and advertised the directly connected networks using the `network` command. Finally, I configured the LAN interfaces as passive using the `passive-interface` command. This prevented RIP from sending routing updates toward the PCs while still allowing the connected LAN networks to be advertised to neighboring routers through the serial interfaces. End-to-end connectivity remained unaffected because only RIP updates were suppressed, not normal data traffic.

---

## Verification

### RIP Configuration

Verified that the LAN interface was configured as a passive interface using:

- `show ip protocols`

### Routing Table

Verified that neighboring routers continued to learn the remote networks using:

- `show ip route`

### Connectivity Test

Verified end-to-end connectivity by successfully pinging from:

- PC1 → PC2
- PC2 → PC1

---

## Skills Learned

- RIP Version 2
- Passive Interface
- Dynamic Routing
- Route Advertisement
- IPv4 Addressing
- Interface Configuration
- Routing Table Verification
- Basic Network Troubleshooting

---

## Devices Used

- 3 × Cisco 2691 Routers
- 2 × Ethernet Switches
- 2 × VPCS Hosts

---

## Files Included

- `RIP Passive Interface.gns3`
- `PC1-config.txt`
- `PC2-config.txt`
- `R1-config.txt`
- `R2-config.txt`
- `R3-config.txt`
- `topology.png`
- `PC1-config.png`
- `PC2-config.png`
- `R1-config.png`
- `R2-config.png`
- `R3-config.png`