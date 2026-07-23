# Phase 3 – Routed Link Between DIST-SW1 and EDGE-R1

## Objective

Establish a Layer 3 point-to-point connection between the Distribution Switch (DIST-SW1) and the Edge Router (EDGE-R1). Configure static routing to enable communication between the internal VLAN networks and the enterprise edge.

---

## Technologies Implemented

- Layer 3 Routed Port
- Point-to-Point Network
- Static Routing
- Default Route

---

## Network Topology

> *Insert the routed link topology image here.*

![Routed Link Topology](topology.png)

---

## Implementation

A dedicated Layer 3 routed link was established between **DIST-SW1** and **EDGE-R1** using the **10.0.0.0/30** network.

Unlike a traditional switchport, the interface connecting the distribution switch to the edge router was converted into a routed port, allowing direct Layer 3 communication between the two devices.

The following configurations were implemented:

- Converted the switch interface into a Layer 3 routed port.
- Assigned IP addresses to both ends of the point-to-point link.
- Configured a default route on **DIST-SW1** pointing to **EDGE-R1**.
- Configured static routes on **EDGE-R1** for all internal VLAN networks.

### Routed Link Addressing

| Device | Interface | IP Address |
| :----: | --------- | ---------- |
| DIST-SW1 | GigabitEthernet1/0/1 | 10.0.0.2/30 |
| EDGE-R1 | GigabitEthernet0/1 | 10.0.0.1/30 |

---

## Verification

### Routed Interface Verification (DIST-SW1)

The routed interface was verified using:

```text
show ip interface brief
```

The verification confirms that:

- The routed interface is configured with the correct IP address.
- The interface is operational (**up/up**).
- All VLAN SVIs remain active after implementing the routed link.

![DIST-SW1 Interface Verification](dist_interface_verification.png)

---

### Routing Table Verification (DIST-SW1)

The routing table was verified using:

```text
show ip route
```

The verification confirms that:

- All enterprise VLAN networks are directly connected.
- The routed point-to-point network (**10.0.0.0/30**) is operational.
- A default route is configured towards **EDGE-R1 (10.0.0.1)** for external network communication.

![DIST-SW1 Routing Table](dist_routing_table.png)

---

### Routing Table Verification (EDGE-R1)

The routing table was verified using:

```text
show ip route
```

The verification confirms that:

- The routed point-to-point network is directly connected.
- Static routes are configured for all enterprise VLAN networks.
- EDGE-R1 can successfully reach every internal subnet through **DIST-SW1 (10.0.0.2)**.

![EDGE-R1 Routing Table](edge_routing_table.png)

---

## Files Included

- `topology.png`
- `dist_interface_verification.png`
- `dist_routing_table.png`
- `edge_routing_table.png`

---

## Result

A dedicated Layer 3 routed link was successfully established between **DIST-SW1** and **EDGE-R1** using the **10.0.0.0/30** point-to-point network. Static routing and a default route were implemented to provide bidirectional communication between the enterprise VLANs and the edge router. This phase establishes the routing foundation required for Internet connectivity, NAT/PAT, and the deployment of enterprise network services in the subsequent phases.