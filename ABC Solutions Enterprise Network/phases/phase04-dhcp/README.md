# Phase 4 – Centralized DHCP Configuration

## Objective

Deploy a centralized DHCP server to automatically assign IP addresses to devices across multiple VLANs. Configure DHCP Relay (IP Helper Address) on the Layer 3 distribution switch to forward DHCP requests from different VLANs to the centralized DHCP server.

---

## Technologies Implemented

- Dynamic Host Configuration Protocol (DHCP)
- Centralized DHCP Server
- DHCP Relay (IP Helper Address)
- Automatic IP Address Allocation

---

## Network Topology

> *Insert the DHCP topology image here.*

![DHCP Topology](topology.png)

---

## Implementation

A centralized DHCP server (SRV1) was configured to provide automatic IP address allocation for all enterprise VLANs.

Since DHCP broadcasts cannot cross Layer 3 boundaries, **DIST-SW1** was configured as a **DHCP Relay Agent** using the `ip helper-address` command on each VLAN interface.

The relay agent forwards DHCP requests from client VLANs to the DHCP server located in the Server VLAN.

### Configured DHCP Pools

| Pool | Network | Default Gateway |
| :--: | :------ | :-------------- |
| HR | 192.168.10.0/24 | 192.168.10.1 |
| Finance | 192.168.20.0/24 | 192.168.20.1 |
| Sales | 192.168.30.0/24 | 192.168.30.1 |
| IT | 192.168.40.0/24 | 192.168.40.1 |
| Management | 192.168.99.0/24 | 192.168.99.1 |
| Servers | 192.168.50.0/24 | 192.168.50.1 |

---

## Verification

### DHCP Server Configuration

The DHCP service was verified on **SRV1**.

The verification confirms that:

- DHCP service is enabled.
- Dedicated DHCP pools exist for each department.
- Correct default gateways and subnet masks are configured.
- Automatic IP address allocation is available for all enterprise VLANs.

![DHCP Server Configuration](dhcp_server_configuration.png)

---

### DHCP Relay Configuration

The relay configuration was verified on **DIST-SW1**.

The verification confirms that:

- `ip helper-address 192.168.50.10` is configured on the required VLAN interfaces.
- DHCP requests from client VLANs are forwarded to the centralized DHCP server.

![DHCP Relay Configuration](dhcp_relay_configuration.png)

---

### DHCP Client Verification

Client devices successfully received IP addresses automatically from the DHCP server.

Example lease information:

| Device | Assigned IP | Default Gateway |
| :----: | :---------- | :-------------- |
| HR-PC2 | 192.168.10.51 | 192.168.10.1 |
| FIN-PC2 | 192.168.20.51 | 192.168.20.1 |

![HR-PC DHCP Lease](hr_pc_dhcp.png)

![Finance-PC DHCP Lease](finance_pc_dhcp.png)

---

### End-to-End Connectivity Verification

Connectivity was verified by testing communication between hosts located in different VLANs.

The successful ping results confirm:

- DHCP address allocation is functioning correctly.
- Inter-VLAN routing is operational.
- Clients from different departments can communicate successfully.

> **Note:** The first ping request may time out due to ARP resolution, which is expected behavior in Cisco Packet Tracer.

![Connectivity Verification](dhcp_connectivity.png)

---

## Files Included

- `topology.png`
- `dhcp_server_configuration.png`
- `dhcp_relay_configuration.png`
- `hr_pc_dhcp.png`
- `finance_pc_dhcp.png`
- `dhcp_connectivity.png`

---

## Result

A centralized DHCP infrastructure was successfully deployed using **SRV1** as the DHCP server and **DIST-SW1** as the DHCP Relay Agent. Client devices across multiple VLANs automatically received valid IP configurations, while successful end-to-end connectivity verified seamless integration with the enterprise routing infrastructure.