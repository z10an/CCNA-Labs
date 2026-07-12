# PAP (Password Authentication Protocol) Lab

## Objective

Configure Password Authentication Protocol (PAP) over a PPP serial link to authenticate routers before allowing communication. Verify successful authentication, test authentication failure scenarios, and understand the limitations of PAP.

---

## Topology

![Topology](topology.png)

---

## Network Addressing

### LAN 1

| Device | IPv4 Address |
|----------|-------------|
| PC1 | 192.168.1.10/24 |
| R1 Fa0/0 | 192.168.1.1/24 |

Default Gateway: **192.168.1.1**

---

### WAN Link

| Device | IPv4 Address |
|----------|-------------|
| R1 Serial1/0 | 10.0.0.1/30 |
| R2 Serial1/0 | 10.0.0.2/30 |

---

### LAN 2

| Device | IPv4 Address |
|----------|-------------|
| R2 Fa0/0 | 192.168.2.1/24 |
| PC2 | 192.168.2.10/24 |

Default Gateway: **192.168.2.1**

---

## Network Policies

The following configuration was implemented:

- Configured PPP encapsulation on the serial link.
- Enabled PAP authentication.
- Configured local username/password database.
- Configured peer authentication credentials.
- Verified successful authentication and end-to-end connectivity.
- Tested authentication failure by using incorrect credentials.

---

## How it Works

PAP is an authentication protocol that operates over PPP.

When the PPP link is established, the peer sends its username and password to the authenticating router.

The router compares the received credentials with its local username database.

- If the credentials match, the PPP session is established.
- If they do not match, authentication fails and the PPP session is rejected.

Unlike CHAP, PAP sends credentials in plain text and performs authentication only once during link establishment.

---

## Verification

### Interface Status

- `show ip interface brief`

### Verify PPP

- `show interfaces serial1/0`

Expected Output:

```
Encapsulation PPP
```

### Verify Configuration

- `show running-config`

### Connectivity Testing

- `ping`

---

## Key Concepts Learned

- PPP Authentication
- Password Authentication Protocol (PAP)
- Local Username Database
- Peer Authentication
- PPP Session Establishment
- Authentication Failure Testing

---

## Engineering Observations

This lab demonstrated several important authentication concepts:

- PAP operates on top of PPP.
- Authentication occurs only during PPP session establishment.
- Credentials are transmitted in plain text.
- PAP requires both routers to agree on authentication parameters.
- Authentication failure prevents the PPP session from being established.

---

## Troubleshooting Experience

During implementation and testing:

- Verified successful PAP authentication.
- Confirmed end-to-end connectivity after successful authentication.
- Tested authentication failure by configuring an incorrect password.
- Observed that changing credentials on an already established PPP session did not immediately interrupt communication.
- Reset the serial interface using `shutdown` and `no shutdown` to force PPP re-authentication.
- Confirmed that authentication failed after renegotiation, resulting in loss of connectivity (`Destination Host Unreachable`).

---

## Skills Learned

- PPP Authentication
- PAP Configuration
- Cisco Local User Database
- WAN Authentication
- Authentication Troubleshooting
- PPP Session Verification

---

## Devices Used

- 2 × Cisco Routers
- 2 × Cisco Switches
- 2 × PCs

---

## Files Included

- `pap-authentication.gns3`
- `R1-config.txt`
- `R2-config.txt`
- `PC1-config.txt`
- `PC2-config.txt`
- `R1-config.png`
- `R2-config.png`
- `topology.png`