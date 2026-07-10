# Dynamic NAT Lab

## Objective

Configure Dynamic Network Address Translation (Dynamic NAT) to translate multiple private IP addresses into addresses selected from a public IP pool while understanding dynamic address allocation and NAT pool operation.

---

## Topology

![Topology](topology.png)

---

## Network Policies

The following NAT policy was implemented:

- Hosts within the 192.168.10.0/24 network are eligible for dynamic NAT translation.
- Public addresses are dynamically assigned from a configured NAT pool.
- Public IP addresses are allocated only when traffic is generated.

---

## How it Works

In this lab, Dynamic NAT was configured using an Access Control List (ACL) to identify inside local addresses eligible for translation. A NAT pool containing available public IP addresses was then created. The router dynamically assigned an available public IP address from the pool whenever an internal host initiated communication with the external network. Once communication ended and the translation expired, the public address became available for reuse by another host.

---

## Verification

### NAT Translation Table

Verified active NAT translations using:

- `show ip nat translations`

### NAT Statistics

Verified NAT operation using:

- `show ip nat statistics`

### Interface Verification

Verified interface configuration using:

- `show ip interface brief`

### Connectivity Test

Verified successful communication between internal hosts and the external server using:

- `ping`

---

## Key Concepts Learned

- Dynamic NAT
- NAT Pools
- Access Lists for NAT
- Dynamic Address Allocation
- Inside Local Address
- Inside Global Address
- NAT Translation Table
- Address Pool Management

---

## Engineering Observations

This lab demonstrated several important characteristics of Dynamic NAT:

- Public IP addresses are allocated only when required.
- Multiple inside hosts can obtain unique public addresses from the configured pool.
- When the pool is exhausted, additional hosts cannot establish new translations until an address becomes available.
- Dynamic NAT provides better public address utilization than Static NAT while still requiring one public address per active host.

---

## Troubleshooting Experience

During implementation and testing, the following tasks were performed:

- Verified ACL configuration used for NAT.
- Confirmed NAT pool configuration.
- Verified dynamic translation entries.
- Tested communication from multiple inside hosts.
- Verified translation statistics after traffic generation.

---

## Skills Learned

- Dynamic NAT Configuration
- NAT Pool Configuration
- ACL-Based NAT
- NAT Verification
- Translation Table Analysis
- NAT Troubleshooting

---

## Devices Used

- 2 × Cisco Routers
- 2 × Ethernet Switches
- 2 × PCs
- 1 × Server

---

## Files Included

- `dynamic-nat.pkt`
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