# Phase 15 – Syslog

## Objective

Implement centralized Syslog logging to collect system events from all routers and switches onto a dedicated Syslog server. Centralized logging enables network administrators to monitor device activity, troubleshoot issues, audit configuration changes, and investigate security events from a single location.

---

## Technologies Implemented

- Syslog
- Centralized Logging
- Remote Logging Server
- Logging Severity Levels
- Event Monitoring

---

## Network Topology

> *Insert the Syslog topology image here.*

![Syslog Topology](topology.png)

---

## Implementation

A centralized Syslog server was enabled on **SRV1** using the Syslog service running at **192.168.50.10**.

All routers and switches within the enterprise network were configured to forward their system log messages to the centralized Syslog server using UDP port 514.

After configuration, each device successfully established communication with the Syslog server and began forwarding operational messages including interface state changes, configuration changes, security events, and system notifications.

---

## Verification

### Syslog Server Verification

The centralized Syslog server was verified to be operational and actively receiving logs from the enterprise network.

The verification confirms:

- Syslog service is enabled.
- Log entries are successfully received from multiple enterprise devices.
- Devices including **ISP-R1**, **EDGE-R1**, **DIST-SW1**, **ACC-SW1**, **ACC-SW2**, and **SRV-SW1** are visible within the log database.
- Multiple event types are successfully collected, including:
  - Configuration changes
  - Interface state changes
  - Logging initialization
  - System notifications
- The centralized logging server is therefore functioning correctly as the enterprise log collector.

![Syslog Server Verification](syslog_server.png)

---

### ISP-R1 Syslog Verification

The ISP router was configured to forward logs to the centralized Syslog server.

The verification confirms:

- Remote Syslog host is configured as **192.168.50.10**.
- Trap logging is enabled at the **Informational** severity level.
- Logging to UDP port **514** is active.
- Logging statistics indicate messages are successfully transmitted.
- The router reports that remote logging has started successfully.
- This confirms the ISP router is forwarding system events to the Syslog server.

![ISP-R1 Syslog Verification](isp-r1_syslog.png)

---

### EDGE-R1 Syslog Verification

The edge router was verified after Syslog configuration.

The verification confirms:

- Syslog is enabled.
- Remote logging destination is configured as **192.168.50.10**.
- Logging is performed using UDP port **514**.
- Trap logging is operating at the Informational severity level.
- Multiple system log messages have been generated and forwarded.
- The local log buffer records interface status changes, confirming that events are being captured before being transmitted to the centralized server.

![EDGE-R1 Syslog Verification](edge-r1_syslog.png)

---

### DIST-SW1 Syslog Verification

The distribution switch was verified after Syslog implementation.

The verification confirms:

- Syslog logging is enabled.
- Remote logging is configured for **192.168.50.10**.
- UDP port **514** is being used.
- Trap logging is active at the Informational level.
- Logging statistics show messages have been successfully transmitted.
- The local log buffer contains VLAN interface events and configuration notifications that are simultaneously forwarded to the centralized Syslog server.

![DIST-SW1 Syslog Verification](dist-sw1_syslog.png)

---

### ACC-SW1 Syslog Verification

The first access switch was verified after Syslog configuration.

The verification confirms:

- Syslog logging is enabled.
- Remote Syslog host is configured correctly.
- Informational trap logging is active.
- Multiple log entries have been generated and transmitted successfully.
- The local log buffer contains operational events including:
  - Interface state transitions
  - Port Security violations
  - Security notifications
- These events demonstrate that security-related incidents are successfully recorded and forwarded to the centralized Syslog server.

![ACC-SW1 Syslog Verification](acc-sw1_syslog.png)

---

### ACC-SW2 Syslog Verification

The second access switch was verified following Syslog implementation.

The verification confirms:

- Syslog logging is enabled.
- Remote logging destination is correctly configured.
- Logging operates through UDP port **514**.
- Informational trap logging is active.
- Local log entries include:
  - VLAN interface state changes
  - GigabitEthernet interface status changes
  - Line protocol state transitions
- These operational events are successfully forwarded to the centralized Syslog server for monitoring.

![ACC-SW2 Syslog Verification](acc-sw2_syslog.png)

---

### SRV-SW1 Syslog Verification

The server access switch was verified after Syslog configuration.

The verification confirms:

- Syslog logging is enabled.
- Remote logging destination is configured correctly.
- Informational trap logging is active.
- Log transmission statistics indicate successful operation.
- The local log buffer records VLAN interface changes and GigabitEthernet interface transitions that are forwarded to the centralized Syslog server.
- This confirms the server switch is fully integrated into the enterprise logging infrastructure.

![SRV-SW1 Syslog Verification](srv-sw1_syslog.png)

---

## Files Included

- `topology.png`
- `syslog_server.png`
- `isp-r1_syslog.png`
- `edge-r1_syslog.png`
- `dist-sw1_syslog.png`
- `acc-sw1_syslog.png`
- `acc-sw2_syslog.png`
- `srv-sw1_syslog.png`

---

## Result

A centralized Syslog infrastructure was successfully deployed across the enterprise network. The dedicated Syslog server received log messages from all routers and switches, providing a single location for monitoring operational events, configuration changes, interface status updates, and security-related incidents. Verification on every network device confirmed successful remote logging to the centralized server, demonstrating a fully functional enterprise logging solution that improves network monitoring, troubleshooting, auditing, and incident analysis.