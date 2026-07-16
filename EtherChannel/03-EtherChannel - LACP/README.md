# EtherChannel - LACP (Link Aggregation Control Protocol)

## Objective

The objective of this lab is to configure a Layer 2 EtherChannel using the Link Aggregation Control Protocol (LACP), verify successful negotiation between two switches, and observe the formation of a logical Port-Channel using the IEEE standard EtherChannel protocol.

---

## Topology

![Topology](topology.png)

---

## Devices Used

- 2 × Cisco 2960 Switches
- Cisco Packet Tracer

---

## Configuration

### SW1

```cisco
enable
configure terminal

interface range fa0/1-2
 channel-group 1 mode active

interface port-channel 1
 switchport mode trunk

end
```

---

### SW2

```cisco
enable
configure terminal

interface range fa0/1-2
 channel-group 1 mode passive

interface port-channel 1
 switchport mode trunk

end
```

---

## Verification Commands

```cisco
show etherchannel summary

show spanning-tree

show interfaces port-channel 1

show running-config interface port-channel 1
```

---

## Verification

### Verify EtherChannel Formation

Confirmed that Port-Channel 1 was successfully created through LACP negotiation.

```
Po1(SU)
```

- **S** = Layer 2 EtherChannel
- **U** = Port-Channel is operational and in use.

---

### Verify Negotiation Protocol

Verified that the EtherChannel was formed using LACP.

```
Protocol : LACP
```

This confirms that the Port-Channel was dynamically negotiated using the IEEE standard protocol.

---

### Verify Member Interfaces

Confirmed that both FastEthernet interfaces were successfully bundled.

```
Fa0/1(P)
Fa0/2(P)
```

- **P** = Interface is successfully bundled into the Port-Channel.

---

### Verify STP Operation

Confirmed that STP recognizes only the logical Port-Channel interface.

Example:

```
Interface        Role Sts Cost
--------------------------------
Po1              Desg FWD
```

The individual member interfaces no longer participate independently in STP.

---

## LACP Negotiation

### Active Mode

```
Active mode.

Initiates LACP negotiation.

Actively sends LACP packets.
```

---

### Passive Mode

```
Passive mode.

Waits for LACP packets.

Does not initiate negotiation.
```

---

## LACP Compatibility

| SW1 | SW2 | Result |
|------|------|--------|
| Active | Active | ✅ EtherChannel Forms |
| Active | Passive | ✅ EtherChannel Forms |
| Passive | Passive | ❌ EtherChannel Does Not Form |

---

## Engineering Observations

- LACP is the IEEE standard protocol for EtherChannel negotiation.
- LACP provides interoperability between networking devices from different vendors.
- At least one side must operate in **Active** mode.
- **Passive** mode waits for LACP packets and does not initiate negotiation.
- LACP automatically verifies compatibility before bundling interfaces.
- STP treats the negotiated Port-Channel as a single logical interface.

---

## Advantages of LACP

- Vendor-independent IEEE standard.
- Automatic EtherChannel negotiation.
- Improved interoperability.
- Increased bandwidth.
- Link redundancy.
- Automatic failover if a member link fails.
- Simplified STP topology.

---

## Practical Use Case

LACP is the preferred EtherChannel protocol in modern enterprise networks, particularly in environments containing networking equipment from multiple vendors. It enables standards-based negotiation while providing increased bandwidth, redundancy, and simplified Layer 2 topology management.

---

## Comparison of EtherChannel Methods

| Method | Negotiation | Standard | Typical Use |
|--------|-------------|----------|-------------|
| Static (`mode on`) | No | No | Small or manually managed networks |
| PAgP | Yes | Cisco Proprietary | Cisco-only environments |
| LACP | Yes | IEEE Standard | Multi-vendor enterprise networks |

---

## Outcome

Successfully configured and verified a Layer 2 EtherChannel using LACP. Confirmed successful negotiation between Active and Passive modes, validated Port-Channel formation, verified STP recognition of the logical Port-Channel, and demonstrated standards-based EtherChannel implementation suitable for modern enterprise networks.