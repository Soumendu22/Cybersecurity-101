# Firewall

## Overview

A **Firewall** is a network security device that monitors and controls incoming and outgoing network traffic based on predefined security rules.

It acts as a **barrier between trusted internal networks and untrusted external networks** such as the internet.

Example:

```text
Internet → Firewall → Internal Network
```

The firewall decides whether traffic should be:

- Allowed
    
- Blocked
    
- Logged
    

---

# Why Firewalls Are Important

Firewalls help protect networks by:

|Purpose|Explanation|
|---|---|
|Prevent unauthorized access|Blocks unknown external connections|
|Control network traffic|Allows only required services|
|Reduce attack surface|Blocks unnecessary ports|
|Monitor traffic|Logs suspicious activity|

Example:

```text
Allow → HTTPS (443)
Allow → HTTP (80)
Block → Telnet (23)
```

---

# Where Firewalls Are Placed

Firewalls are typically placed at the **network perimeter**.

Example architecture:

```text
Internet
   ↓
Firewall
   ↓
Internal Network
```

Enterprise environments may use multiple firewalls:

```text
Internet
   ↓
Perimeter Firewall
   ↓
DMZ
   ↓
Internal Firewall
   ↓
Internal Network
```

---

# Firewall Rule Structure

Firewall rules determine what traffic is allowed.

Example rule:

|Source|Destination|Port|Action|
|---|---|---|---|
|Any|Web Server|80|Allow|
|Any|Internal Network|23|Block|

Example configuration:

```text
ALLOW TCP 80
ALLOW TCP 443
DENY TCP 23
```

---

# Types of Firewalls

## Packet Filtering Firewall

This is the **simplest firewall type**.

It filters packets based on:

- IP address
    
- Port
    
- Protocol
    

Example check:

```text
Source IP
Destination IP
Port
Protocol
```

Advantages:

- Fast
    
- Low resource usage
    

Disadvantages:

- Cannot inspect packet content
    

---

## Stateful Firewall

A **stateful firewall** tracks the state of active connections.

Example:

```text
Client → Request
Server → Response
```

Firewall remembers connection state.

Advantages:

- More secure
    
- Understands sessions
    

Example:

```text
Established connections allowed automatically
```

---

## Proxy Firewall (Application Firewall)

Acts as an intermediary between client and server.

Example:

```text
Client → Proxy Firewall → Server
```

The firewall analyzes **application layer traffic**.

Advantages:

- Deep packet inspection
    
- High security
    

Disadvantages:

- Slower
    

---

## Next Generation Firewall (NGFW)

Modern firewalls combine multiple security technologies.

Features:

- Deep packet inspection
    
- Intrusion prevention
    
- Application awareness
    
- Malware detection
    

Example vendors:

- Palo Alto
    
- Fortinet
    
- Cisco
    

---

# Firewall Filtering Methods

Firewalls inspect packets using different methods.

## IP Filtering

Blocks or allows traffic based on IP address.

Example:

```text
Block → 192.168.10.5
```

---

## Port Filtering

Controls access based on ports.

Example:

|Port|Service|
|---|---|
|80|HTTP|
|443|HTTPS|
|22|SSH|

Example rule:

```text
Allow port 80
Block port 23
```

---

## Protocol Filtering

Allows or blocks protocols.

Example:

|Protocol|Use|
|---|---|
|TCP|Web traffic|
|UDP|DNS|
|ICMP|Ping|

Example:

```text
Block ICMP
```

---

# Firewall Zones

Modern firewalls use **security zones**.

Example:

|Zone|Description|
|---|---|
|Internal|Trusted network|
|External|Internet|
|DMZ|Public servers|

Example architecture:

```text
Internet
   ↓
Firewall
   ↓
DMZ (Web Server)
   ↓
Internal Network
```

---

# Common Firewall Technologies

## iptables (Linux)

Example rule:

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Block port:

```bash
iptables -A INPUT -p tcp --dport 23 -j DROP
```

---

## ufw (Ubuntu Firewall)

Enable firewall:

```bash
ufw enable
```

Allow SSH:

```bash
ufw allow 22
```

---

# Firewall Logging

Firewalls log network activity.

Example log entry:

```text
Blocked connection from 203.0.113.45 to port 23
```

Logs help in:

- Threat detection
    
- Incident response
    
- Forensics analysis
    

---

# Firewall in Cybersecurity

Firewalls protect against:

|Threat|Description|
|---|---|
|Unauthorized access|Block external attackers|
|Malware communication|Block C2 servers|
|Port scanning|Detect scanning attempts|
|DoS attacks|Rate limit traffic|

Example detection:

```text
Multiple connection attempts to port 22
```

---

# Limitations of Firewalls

Firewalls cannot stop all attacks.

Limitations include:

|Limitation|Explanation|
|---|---|
|Insider threats|Internal attackers bypass firewall|
|Encrypted traffic|Harder to inspect|
|Social engineering|Not network-based|

---

# Summary

|Concept|Meaning|
|---|---|
|Firewall|Network traffic filter|
|Packet filtering|Basic filtering|
|Stateful firewall|Tracks connections|
|Proxy firewall|Application inspection|
|NGFW|Advanced firewall|

---