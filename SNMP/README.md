# SNMP (Simple Network Management Protocol)

## Objective

Configure and verify basic SNMPv2c communication on a Cisco router using Read-Only (RO) and Read-Write (RW) community strings. This lab demonstrates how network management systems (NMS) securely access management information stored on Cisco devices using Object Identifiers (OIDs).

---

# Topology

![Topology](topology.png)

---

# Network Addressing

| Device | Interface | IP Address | Role |
|----------|-----------|---------------|---------------------------|
| R1 | GigabitEthernet0/0 | 192.168.10.1/24 | Managed Device (SNMP Agent) |
| PC | FastEthernet0 | 192.168.10.2/24 | Network Management System (NMS) |

Default Gateway

```
Not Required
```

---

# Network Policies

- SNMP Version 2c is used.
- Read-Only (RO) community allows monitoring only.
- Read-Write (RW) community allows both monitoring and configuration changes.
- The router acts as the SNMP Agent.
- The PC acts as the Network Management System (NMS).

---

# How it Works

1. The router is configured with SNMP community strings.
2. The Network Management System authenticates using the configured community.
3. The NMS sends SNMP requests to the router.
4. The SNMP Agent retrieves the requested Management Information Base (MIB) objects.
5. The router returns the requested information to the NMS.
6. When using the Read-Write community, the NMS can also modify supported MIB objects on the router.

---

# Configuration

## Router

```cisco
interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

snmp-server community Cisco1 RO
snmp-server community Cisco2 RW
```

---

# Verification

## Verify SNMP Configuration

```cisco
show running-config | include snmp
```

Verified:

- Read-Only community configured.
- Read-Write community configured.

---

## Verify SNMP GET Operations

Successfully retrieved the following MIB objects from the router:

- System Name (`sysName`)
- System Uptime (`sysUpTime`)
- Interface Description (`ifDescr`)
- Interface Number (`ifNumber`)
- Interface Type (`ifType`)
- Interface Administrative Status (`ifAdminStatus`)

---

## Verify SNMP SET Operation

Using the Read-Write community:

- Modified the router hostname (`sysName`) remotely.
- Confirmed the hostname change through SNMP.

---

# Key Concepts Learned

- SNMP
- SNMP Agent
- Network Management System (NMS)
- Management Information Base (MIB)
- Object Identifier (OID)
- SNMP GET
- SNMP SET
- Read-Only Community
- Read-Write Community
- SNMPv2c

---

# Engineering Observations

SNMP provides centralized visibility into network devices without requiring administrators to log into every router or switch individually. Instead of manually checking operational information, a Network Management System can retrieve device statistics, interface information, and system health using standardized MIB objects.

Read-Only communities are typically used for monitoring, while Read-Write communities allow remote configuration changes. In production environments, SNMPv3 is generally preferred because it provides authentication and encryption, addressing the security limitations of SNMPv1 and SNMPv2c.

---

# Troubleshooting Experience

### Issue

Packet Tracer provides only a limited implementation of SNMP compared to real Cisco IOS and enterprise Network Management Systems.

### Cause

The Packet Tracer SNMP simulator supports only a subset of Management Information Base (MIB) objects and basic GET/SET operations.

### Resolution

Configured SNMPv2c community strings and successfully verified supported GET operations and a SET operation by modifying the router hostname.

### Verification

- SNMP communities successfully configured.
- Multiple MIB objects retrieved through SNMP GET.
- Router hostname successfully modified through SNMP SET using the Read-Write community.

---

# Skills Learned

- Configure SNMPv2c on Cisco IOS
- Configure Read-Only and Read-Write communities
- Understand SNMP Agent and NMS communication
- Retrieve information using SNMP GET
- Modify supported objects using SNMP SET
- Interpret common MIB objects
- Verify SNMP configuration on Cisco devices
- Understand enterprise network monitoring concepts

---

# Devices Used

- Cisco 2911 Router
- PC (Network Management System)
- Cisco Packet Tracer

---

# Files Included

- topology.png
- R1-config.png
- sysName.png
- sysUpTime.png
- ifDescr.png
- ifNumber.png
- ifType.png
- ifAdminStatus.png
- sysName-SET-1.png
- sysName-SET-2.png
- SNMP.pkt
- README.md