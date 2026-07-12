# CHAP (Challenge Handshake Authentication Protocol) Lab

## Objective

Configure Challenge Handshake Authentication Protocol (CHAP) over a PPP serial link to securely authenticate peer routers before establishing communication. Verify successful authentication, test authentication failures, and understand how CHAP improves security compared to PAP.

---

## Topology

![Topology](topology.png)

---

## Network Addressing

### LAN 1

| Device | IPv4 Address |
|----------|-------------|
| PC1 | 192.168.1.10/24 |
| R1 G0/0 | 192.168.1.1/24 |

Default Gateway: **192.168.1.1**

---

### WAN Link

| Device | IPv4 Address |
|----------|-------------|
| R1 S0/0/0 | 10.0.0.1/30 |
| R2 S0/0/0 | 10.0.0.2/30 |

---

### LAN 2

| Device | IPv4 Address |
|----------|-------------|
| R2 G0/0 | 192.168.2.1/24 |
| PC2 | 192.168.2.10/24 |

Default Gateway: **192.168.2.1**

---

## Network Policies

The following configuration was implemented:

- Configured PPP encapsulation on the serial link.
- Enabled CHAP authentication.
- Configured local username/password database.
- Used router hostnames as CHAP identities.
- Verified successful authentication and end-to-end connectivity.
- Tested authentication failure using incorrect credentials.

---

## How it Works

CHAP authenticates routers using a **challenge-response mechanism**.

When the PPP session starts, the authenticating router sends a random challenge to its peer.

The peer combines the challenge with its shared secret (password), computes a hash, and sends the hash back.

The authenticating router performs the same calculation using its locally configured password.

- If both hashes match, authentication succeeds.
- If they do not match, the PPP session is rejected.

Unlike PAP, the actual password is **never transmitted** across the link.

CHAP also performs **periodic re-authentication**, making it more secure than PAP.

---

## Verification

### Interface Status

- `show ip interface brief`

### Verify PPP

- `show interfaces serial0/0/0`

Expected Output:

```
Encapsulation PPP
LCP Open
```

### Verify Configuration

- `show running-config`

### Connectivity Testing

- `ping`

---

## Key Concepts Learned

- Point-to-Point Protocol (PPP)
- Challenge Handshake Authentication Protocol (CHAP)
- Challenge-Response Authentication
- Hostname-Based Authentication
- Local Username Database
- Secure WAN Authentication

---

## Engineering Observations

This lab demonstrated several important authentication concepts:

- CHAP operates on top of PPP.
- CHAP never sends passwords in plain text.
- Routers authenticate using a challenge-response mechanism.
- Router hostnames must exactly match the peer's configured username.
- CHAP periodically re-authenticates peers during the session.
- Authentication failure prevents the PPP session from being established.

---

## Troubleshooting Experience

During implementation and testing:

- Verified successful CHAP authentication.
- Confirmed end-to-end connectivity after authentication.
- Tested authentication failure by configuring an incorrect shared secret.
- Reset the PPP session using `shutdown` and `no shutdown` to force re-authentication.
- Observed authentication failure when credentials did not match.
- Verified that matching usernames, passwords, and router hostnames restored connectivity.

---

## PAP vs CHAP

| Feature | PAP | CHAP |
|----------|-----|------|
| Password sent in plain text | Yes | No |
| Uses Challenge-Response | No | Yes |
| Periodic Re-authentication | No | Yes |
| Security | Low | High |

---

## Skills Learned

- PPP Authentication
- CHAP Configuration
- Secure WAN Authentication
- Cisco Username Database
- Authentication Troubleshooting
- PPP Session Verification

---

## Devices Used

- 2 × Cisco Routers
- 2 × Cisco Switches
- 2 × PCs

---

## Files Included

- `chap-authentication.gns3`
- `R1-config.txt`
- `R2-config.txt`
- `PC1-config.txt`
- `PC2-config.txt`
- `R1-config.png`
- `R2-config.png`
- `topology.png`
