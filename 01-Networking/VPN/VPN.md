# VPN (Virtual Private Network)

## Overview

A **Virtual Private Network (VPN)** creates a secure and encrypted connection between a user and a remote network over the internet.

It allows users to securely access private networks even when using public internet connections.

Example:

```text
User → Encrypted Tunnel → VPN Server → Internet
```

Without VPN:

```text
User → Internet → Website
```

With VPN:

```text
User → Encrypted Tunnel → VPN Server → Website
```

The VPN encrypts the traffic so attackers cannot easily read it.

---

# Why VPN is Used

VPN provides multiple security and privacy benefits.

|Purpose|Description|
|---|---|
|Privacy|Hide user's IP address|
|Security|Encrypt internet traffic|
|Remote access|Access company network remotely|
|Bypass restrictions|Access geo-restricted content|

Example use case:

```text
Employee → VPN → Company Network
```

---

# How VPN Works

A VPN creates an **encrypted tunnel** between the client and VPN server.

Steps:

1 User connects to VPN client  
2 VPN client authenticates with VPN server  
3 Encrypted tunnel is created  
4 All traffic goes through VPN server

Example flow:

```text
User Device
     ↓
Encrypted Tunnel
     ↓
VPN Server
     ↓
Internet
```

---

# VPN Tunneling

VPN uses **tunneling protocols** to encapsulate and encrypt traffic.

Tunneling means:

```text
Original packet → Encrypted → Sent through secure tunnel
```

The data becomes unreadable to attackers.

---

# Common VPN Protocols

## PPTP (Point-to-Point Tunneling Protocol)

One of the oldest VPN protocols.

|Feature|Description|
|---|---|
|Encryption|Weak|
|Speed|Fast|
|Security|Outdated|

Port:

```text
1723
```

---

## L2TP (Layer 2 Tunneling Protocol)

Often combined with IPSec for encryption.

Example:

```text
L2TP + IPSec
```

Provides stronger security than PPTP.

---

## IPSec (Internet Protocol Security)

IPSec secures IP communications by encrypting packets.

Two main modes:

|Mode|Description|
|---|---|
|Transport Mode|Encrypts payload only|
|Tunnel Mode|Encrypts entire packet|

Used in **site-to-site VPNs**.

---

## OpenVPN

Open-source VPN protocol.

Features:

- Strong encryption
    
- Highly configurable
    
- Widely used
    

Port:

```text
1194
```

---

## WireGuard

Modern VPN protocol.

Advantages:

- Very fast
    
- Strong encryption
    
- Simple design
    

Used in many modern VPN services.

---

# Types of VPN

## Remote Access VPN

Allows individual users to connect to a private network remotely.

Example:

```text
Laptop → VPN → Company Network
```

Used by remote employees.

---

## Site-to-Site VPN

Connects entire networks together.

Example:

```text
Office A Network
      ↓
    VPN
      ↓
Office B Network
```

Used by organizations with multiple branches.

---

# VPN Encryption

VPN uses encryption algorithms to protect traffic.

Common algorithms:

|Algorithm|Purpose|
|---|---|
|AES|Strong encryption|
|SHA|Data integrity|
|RSA|Key exchange|

Example process:

```text
Data → Encryption → Secure Tunnel → Decryption
```

---

# VPN Components

Important components in VPN infrastructure.

|Component|Purpose|
|---|---|
|VPN Client|Software on user device|
|VPN Server|Handles encrypted connections|
|Encryption|Secures data|
|Authentication|Verifies users|

---

# VPN in Cybersecurity

VPNs are used to:

|Use|Description|
|---|---|
|Secure remote work|Employees access company networks|
|Protect public WiFi usage|Encrypt traffic|
|Hide user IP|Improve privacy|
|Secure communications|Prevent interception|

Example secure connection:

```text
User → VPN → Company Server
```

---

# VPN Security Risks

VPN can also introduce risks.

|Risk|Description|
|---|---|
|Misconfiguration|Weak security settings|
|Compromised VPN servers|Data interception|
|VPN leaks|IP address exposure|
|Credential theft|Unauthorized access|

---

# VPN vs Proxy

|Feature|VPN|Proxy|
|---|---|---|
|Encryption|Yes|Usually no|
|IP masking|Yes|Yes|
|Security|High|Low|
|Traffic protection|All traffic|Specific apps|

---

# Example VPN Connection

Connecting using OpenVPN:

```bash
sudo openvpn config.ovpn
```

---

# Summary

|Concept|Meaning|
|---|---|
|VPN|Secure encrypted connection|
|Tunnel|Secure communication path|
|Encryption|Protects data|
|Remote VPN|Individual access|
|Site-to-site VPN|Network-to-network connection|

---