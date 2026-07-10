# PAT (NAT Overload) Lab

## Objective

Configure Port Address Translation (PAT), also known as NAT Overload, to allow multiple internal hosts to share a single public IP address while understanding how port numbers enable simultaneous communication with external networks.

---

## Topology

![Topology](topology.png)

---

## Network Policies

The following NAT policy was implemented:

- Hosts within the 192.168.10.0/24 network are eligible for NAT translation.
- All translated hosts share the public IP address assigned to the outside interface.
- Port numbers are used to uniquely identify individual communication sessions.
- Multiple internal hosts can simultaneously access external resources using a single public IP address.

---

## How it Works

In this lab, PAT (Port Address Translation) was configured using an Access Control List (ACL) to identify the internal network eligible for translation. Instead of assigning each host a unique public IP address, the router translated all internal hosts to the IP address configured on the outside interface using the `overload` option.

When multiple hosts initiated communication simultaneously, the router differentiated each session by assigning unique transport-layer port numbers. Incoming return traffic was matched against the NAT translation table, allowing the router to forward each packet to the correct internal host.

---

## Verification

### NAT Translation Table

Verified active NAT translations using:

- `show ip nat translations`

### NAT Statistics

Verified NAT operation using:

- `show ip nat statistics`

### Interface Verification

Verified NAT interface configuration using:

- `show ip interface brief`

### Connectivity Test

Verified successful communication between internal hosts and the external server using:

- `ping`

---

## Key Concepts Learned

- Port Address Translation (PAT)
- NAT Overload
- Interface-Based NAT
- ACL-Based NAT
- Port Number Translation
- Inside Local Address
- Inside Global Address
- NAT Translation Table
- NAT Statistics

---

## Engineering Observations

This lab demonstrated several important characteristics of PAT:

- Multiple internal hosts can share a single public IP address.
- The router differentiates simultaneous connections using transport-layer port numbers.
- PAT significantly conserves public IPv4 addresses compared to Static NAT and Dynamic NAT.
- The outside interface IP address is commonly used as the public translation address.
- PAT is the most widely deployed NAT implementation in enterprise and home networks.

---

## Troubleshooting Experience

During implementation and testing, the following tasks were performed:

- Verified ACL configuration used for NAT.
- Confirmed inside and outside NAT interface assignments.
- Verified active translation entries.
- Generated traffic from multiple hosts simultaneously.
- Verified successful address and port translation using NAT show commands.

---

## Skills Learned

- PAT Configuration
- NAT Overload Configuration
- ACL-Based NAT
- Port Address Translation
- NAT Verification
- Translation Table Analysis
- NAT Troubleshooting
- Enterprise Edge Router Configuration

---

## Devices Used

- 2 × Cisco Routers
- 2 × Ethernet Switches
- 2 × PCs
- 1 × Server

---

## Files Included

- `pat-nat-overload.pkt`
- `R1-config.txt`
- `R2-config.txt`
- `PC1-config.txt`
- `PC2-config.txt`
- `Server-config.txt`
- `R1-config.png`
- `R2-config.png`
- `PC1-config.png`
- `PC2-config.png`
- `Server-config.png`
- `topology.png`