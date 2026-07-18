# Domain Name System (DNS)

## Objective

Design and implement a centralized Domain Name System (DNS) service in a small enterprise network where a dedicated DNS server provides hostname resolution for Cisco network devices.

This lab demonstrates how DNS improves network management by allowing administrators to access devices using meaningful hostnames instead of IP addresses.

---

# Topology

![Topology](topology.png)

---

# Network Addressing

| Device | Interface | IP Address | Role |
|----------|-----------|---------------|----------------|
| R1 | G0/0 | 192.168.1.1/24 | Router |
| Core-SW | VLAN 1 | 192.168.1.2/24 | DNS Client |
| SW1 | VLAN 1 | 192.168.1.3/24 | DNS Client |
| SW2 | VLAN 1 | 192.168.1.4/24 | DNS Client |
| Server1 | FastEthernet0 | 192.168.1.10/24 | DNS Server |

Default Gateway (Switches & Server)

```
192.168.1.1
```

DNS Server

```
192.168.1.10
```

---

# Network Policies

- A dedicated server provides DNS services.
- All Cisco devices use the centralized DNS server.
- Static A Records are created for every network device.
- Devices resolve hostnames before initiating communication.
- DNS is used only for hostname resolution.

---

# How it Works

1. The DNS service is enabled on the server.
2. Static DNS A Records are created for all network devices.
3. Cisco devices are configured to use the DNS server.
4. When a hostname is entered, the device queries the DNS server.
5. The DNS server returns the corresponding IP address.
6. Communication is then established using the resolved IP address.

---

# DNS Records

| Hostname | IP Address |
|-----------|------------|
| r1.company.local | 192.168.1.1 |
| core.company.local | 192.168.1.2 |
| sw1.company.local | 192.168.1.3 |
| sw2.company.local | 192.168.1.4 |

---

# Verification

## Cisco Devices

```
ping r1.company.local
ping core.company.local
ping sw1.company.local
ping sw2.company.local
```

Verified:

- Hostnames successfully resolved.
- Successful ICMP connectivity.
- Cisco devices communicating using DNS.
- DNS server responding correctly to client queries.

---

# Key Concepts Learned

- Domain Name System (DNS)
- DNS Server
- DNS Client
- Hostname Resolution
- A Records
- Name Resolution Process
- IP Address Mapping
- Centralized Name Services

---

# Engineering Observations

DNS improves network usability by allowing administrators to reference devices using descriptive hostnames rather than numerical IP addresses.

In enterprise environments, DNS reduces configuration errors, simplifies management, and makes troubleshooting more efficient. Many network services—including SSH, web management interfaces, monitoring platforms, and automation tools—depend on reliable hostname resolution.

Using a centralized DNS server also provides a single location for maintaining network name records, making future changes easier to manage.

---

# Troubleshooting Experience

### Issue

Hostname resolution failed until Cisco devices were configured with the correct DNS server address.

### Cause

Without a configured DNS server, Cisco devices attempt to resolve hostnames locally and cannot translate names into IP addresses.

### Resolution

- Configured the DNS server with static A Records.
- Configured every Cisco device to use the centralized DNS server.
- Verified successful hostname resolution using ping commands.

### Verification

- DNS service enabled successfully.
- A Records created for all network devices.
- Cisco devices successfully resolved hostnames.
- Network connectivity verified using DNS names instead of IP addresses.

---

# Skills Learned

- Configure a DNS server in Packet Tracer
- Create DNS A Records
- Configure Cisco devices as DNS clients
- Verify hostname resolution
- Troubleshoot DNS configuration
- Design centralized name resolution services
- Understand enterprise DNS implementation

---

# Devices Used

- Cisco 2911 Router
- Cisco Catalyst 2960 Switches
- Packet Tracer Server
- Cisco Packet Tracer

---

# Files Included

- topology.png
- DNS.pkt
- README.md