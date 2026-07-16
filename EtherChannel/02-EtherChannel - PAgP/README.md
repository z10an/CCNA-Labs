# EtherChannel - PAgP (Port Aggregation Protocol)

## Objective

The objective of this lab is to configure a Layer 2 EtherChannel using Cisco's Port Aggregation Protocol (PAgP), verify successful negotiation between two switches, and observe the formation of a logical Port-Channel through dynamic negotiation rather than manual configuration.

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
 channel-group 1 mode auto

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
 channel-group 1 mode desirable

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

Confirmed that Port-Channel 1 was successfully created through PAgP negotiation.

```
Po1(SU)
```

- **S** = Layer 2 EtherChannel
- **U** = Port-Channel is operational and in use

---

### Verify Negotiation Protocol

Verified that the EtherChannel was formed using Cisco's Port Aggregation Protocol.

```
Protocol : PAgP
```

This confirms that the bundle was dynamically negotiated rather than statically configured.

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

The individual physical interfaces no longer participate independently in STP.

---

## PAgP Negotiation

### Auto Mode

```
Passive mode.

Waits for PAgP negotiation.

Does not initiate negotiation.
```

---

### Desirable Mode

```
Active mode.

Initiates PAgP negotiation.

Sends PAgP packets to form an EtherChannel.
```

---

## PAgP Compatibility

| SW1 | SW2 | Result |
|------|------|--------|
| Desirable | Desirable | ✅ EtherChannel Forms |
| Desirable | Auto | ✅ EtherChannel Forms |
| Auto | Auto | ❌ EtherChannel Does Not Form |

---

## Engineering Observations

- PAgP is Cisco's proprietary EtherChannel negotiation protocol.
- PAgP automatically negotiates EtherChannel formation between Cisco switches.
- At least one side must operate in **Desirable** mode.
- **Auto** mode never initiates negotiation and only responds to received PAgP packets.
- PAgP helps prevent configuration mismatches compared to Static EtherChannel.
- STP treats the negotiated Port-Channel as a single logical interface.

---

## Advantages of PAgP

- Automatic EtherChannel negotiation.
- Reduced risk of manual configuration errors.
- Increased bandwidth.
- Link redundancy.
- Simplified Layer 2 topology for STP.

---

## Practical Use Case

PAgP is commonly used in Cisco-only environments where dynamic negotiation is preferred over manually forcing EtherChannel formation. It provides a safer deployment by verifying compatibility before bundling interfaces.

---

## Outcome

Successfully configured and verified a Layer 2 EtherChannel using PAgP. Confirmed successful negotiation between Auto and Desirable modes, validated Port-Channel formation, and verified that STP recognizes the logical Port-Channel instead of individual physical links.