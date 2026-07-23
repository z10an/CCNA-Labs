# Phase 14 – Network Time Protocol (NTP)

## Objective

Implement Network Time Protocol (NTP) to synchronize the clocks of network devices using the ISP router as the enterprise time source. Consistent time synchronization is essential for accurate log timestamps, event correlation, troubleshooting, and network monitoring.

---

## Technologies Implemented

- Network Time Protocol (NTP)
- NTP Master
- NTP Client
- Clock Timezone Configuration
- Centralized Time Synchronization

---

## Network Topology

> *Insert the NTP topology image here.*

![NTP Topology](topology.png)

---

## Implementation

The ISP router was configured as the enterprise NTP Master (Stratum 1) after manually setting the correct system date and time.

All enterprise network devices were configured as NTP clients using the ISP router (209.165.200.226) as their time source. Additionally, the IST timezone was configured on every device to ensure timestamps match the organization's local time.

Packet Tracer successfully synchronized **ACC-SW1** with the NTP server. However, despite identical configurations and full IP connectivity, **EDGE-R1**, **DIST-SW1**, **ACC-SW2**, and **SRV-SW1** remained unsynchronized.

This behavior is a known limitation of Cisco Packet Tracer's NTP implementation rather than a configuration issue, as connectivity, server configuration, and client configuration were verified successfully.

---

## Verification

### ISP-R1 NTP Server Verification

The ISP router was verified as the enterprise NTP server.

The verification confirms:

- The system clock was manually configured with the correct **date and time**.
- NTP Master mode is enabled using **Stratum 1**.
- `show ntp associations` confirms the router is synchronized with its local hardware clock (127.127.1.1).
- `show ntp status` reports:
  - **Clock is synchronized**
  - **Stratum 1**
  - Reference clock **127.127.1.1**
  - Loop state **CTRL (Normal Controlled Loop)**
- The router is therefore functioning correctly as the centralized enterprise time source.

![ISP-R1 NTP Verification](isp-r1_ntp.png)

---

### EDGE-R1 NTP Client Verification

The edge router was configured as an NTP client.

The verification confirms:

- IST timezone was successfully configured.
- The correct NTP server (**209.165.200.226**) is configured.
- IP connectivity to the NTP server was verified successfully using ICMP ping.
- `show ntp associations` detects the configured server but remains in the **INIT** state.
- `show ntp status` reports:
  - Unsynchronized
  - Stratum 16
  - No reference clock
  - Never updated
- Since connectivity and configuration are both correct, this behavior is attributed to a Packet Tracer NTP synchronization limitation rather than a configuration error.

![EDGE-R1 NTP Verification](edge-r1_ntp.png)

---

### DIST-SW1 NTP Client Verification

The distribution switch was configured as an NTP client.

The verification confirms:

- IST timezone was configured successfully.
- The NTP server is correctly configured as **209.165.200.226**.
- `show ntp associations` lists the configured server but shows the **INIT** state.
- `show ntp status` indicates:
  - Unsynchronized
  - Stratum 16
  - No reference clock
  - Never updated
- The configuration matches the remaining enterprise devices, indicating the observed synchronization failure is caused by Packet Tracer rather than incorrect configuration.

![DIST-SW1 NTP Verification](dist-sw1_ntp.png)

---

### ACC-SW1 NTP Client Verification

The access switch **ACC-SW1** successfully synchronized with the enterprise NTP server.

The verification confirms:

- IST timezone was configured successfully.
- The correct NTP server is configured.
- `show ntp associations` displays the ISP router as the active synchronization source.
- `show clock` displays the correct synchronized date and time.
- `show ntp status` reports:
  - Clock synchronized
  - Stratum 2
  - Reference clock **209.165.200.226**
  - Normal Controlled Loop (CTRL)
  - Recent successful synchronization updates
- This confirms that the NTP server configuration is fully operational within the Packet Tracer environment.

![ACC-SW1 NTP Verification](acc-sw1_ntp.png)

---

### ACC-SW2 NTP Client Verification

The second access switch was configured as an NTP client.

The verification confirms:

- IST timezone was configured successfully.
- The correct NTP server is configured.
- `show ntp associations` shows the configured server in the **INIT** state.
- `show ntp status` reports:
  - Unsynchronized
  - Stratum 16
  - No reference clock
  - Never updated
- Since the configuration is identical to ACC-SW1, the inconsistent synchronization behavior is attributed to Packet Tracer limitations.

![ACC-SW2 NTP Verification](acc-sw2_ntp.png)

---

### SRV-SW1 NTP Client Verification

The server switch was also configured as an NTP client.

The verification confirms:

- IST timezone was configured successfully.
- The enterprise NTP server is correctly configured.
- `show ntp associations` detects the configured server but remains in the **INIT** state.
- `show ntp status` reports:
  - Unsynchronized
  - Stratum 16
  - No reference clock
  - Never updated
- The observed behavior is consistent with other Packet Tracer devices that fail to synchronize despite correct configuration and connectivity.

![SRV-SW1 NTP Verification](srv-sw1_ntp.png)

---

## Files Included

- `topology.png`
- `isp-r1_ntp.png`
- `edge-r1_ntp.png`
- `dist-sw1_ntp.png`
- `acc-sw1_ntp.png`
- `acc-sw2_ntp.png`
- `srv-sw1_ntp.png`

---

## Result

A centralized NTP infrastructure was successfully implemented using the ISP router as the enterprise time server. The NTP server was verified to operate correctly as a synchronized Stratum 1 source, and all enterprise devices were configured to use it for time synchronization. Packet Tracer successfully synchronized ACC-SW1, confirming the server configuration was functional. Although the remaining devices did not synchronize despite correct configuration and verified connectivity, this behavior is consistent with known Packet Tracer limitations rather than configuration errors. The enterprise network is therefore correctly configured for centralized time synchronization in accordance with standard Cisco NTP deployment practices.