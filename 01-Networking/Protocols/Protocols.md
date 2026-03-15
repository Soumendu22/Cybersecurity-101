# Networking Protocols 

## Overview

A **protocol** is a set of rules that defines how devices communicate over a network.

Protocols define:

- Data format
    
- Transmission method
    
- Error handling
    
- Security mechanisms
    

Protocols operate across different **OSI layers**.

---

# Transport Layer Protocols

## TCP (Transmission Control Protocol)

### Port

Multiple ports depending on application

### Purpose

Reliable communication between systems.

### Features

|Feature|Description|
|---|---|
|Connection oriented|Requires handshake|
|Reliable|Ensures delivery|
|Ordered|Maintains packet order|

### TCP 3-Way Handshake

```
Client → SYN
Server → SYN-ACK
Client → ACK
```

### Used In

- SSH
    
- FTP
    
- SMTP
    
- Email protocols
    

---

## UDP (User Datagram Protocol)

### Purpose

Fast communication without reliability.

### Features

|Feature|Description|
|---|---|
|Connectionless|No handshake|
|Faster|Less overhead|
|Unreliable|Packets may drop|

### Used In

- Streaming
    
- Online gaming
    
- DNS queries
    
- VoIP
    

---

# Network Layer Protocols

## IP (Internet Protocol)

### Purpose

Provides logical addressing and packet routing.

### Types

|Version|Description|
|---|---|
|IPv4|32-bit addressing|
|IPv6|128-bit addressing|

Example:

```
192.168.1.1
```

### Working

1. Data divided into packets
    
2. Each packet gets source and destination IP
    
3. Routers forward packets
    

---

## ICMP (Internet Control Message Protocol)

### Purpose

Used for **network diagnostics and error messages**.

### Example

Ping command:

```
ping google.com
```

### Message Types

|Type|Use|
|---|---|
|Echo request|Ping request|
|Echo reply|Ping response|
|Destination unreachable|Network error|

### Security Risk

Attackers use ICMP for:

- Network mapping
    
- ICMP flood attacks
    

---

## ARP (Address Resolution Protocol)

### Purpose

Maps **IP address to MAC address**.

### Working

1. Device broadcasts ARP request
    
2. Target device responds with MAC address
    

Example:

```
Who has 192.168.1.1?
```

### Security Risk

ARP poisoning attacks.

---

# Data Link Layer Protocols

## Ethernet

### Purpose

Standard for wired local area networks.

### Features

|Feature|Description|
|---|---|
|Frame-based communication|Data transmitted as frames|
|Uses MAC addresses|Hardware addressing|

Example frame fields:

- Source MAC
    
- Destination MAC
    
- Payload
    

---

## PPP (Point-to-Point Protocol)

### Purpose

Direct communication between two nodes.

Used in:

- Dial-up connections
    
- VPN connections
    

---

# File Transfer Protocols

## FTP (File Transfer Protocol)

### Ports

|Port|Purpose|
|---|---|
|21|Control|
|20|Data|

### Purpose

Transfers files between client and server.

### Working

1. Client connects to server
    
2. Authentication
    
3. File upload/download
    

### Security Issue

FTP sends data **in plaintext**.

---

## TFTP (Trivial File Transfer Protocol)

### Port

```
69
```

### Purpose

Simplified file transfer protocol.

Used in:

- Network booting
    
- Firmware updates
    

---

# Remote Access Protocols

## SSH (Secure Shell)

### Port

```
22
```

### Purpose

Secure remote system administration.

### Features

- Encrypted communication
    
- Secure login
    
- Secure file transfer
    

### Example

```
ssh user@server-ip
```

---

## Telnet

### Port

```
23
```

### Purpose

Remote login protocol.

### Problem

Telnet sends **credentials in plaintext**, making it insecure.

---

# Email Protocols

## SMTP (Simple Mail Transfer Protocol)

### Ports

|Port|Use|
|---|---|
|25|Mail transfer|
|587|Mail submission|

### Purpose

Used for **sending emails**.

### Working

```
Client → Mail Server → Recipient Server
```

---

## POP3 (Post Office Protocol)

### Port

```
110
```

### Purpose

Retrieve emails from mail server.

### Feature

Downloads emails to local device.

---

## IMAP (Internet Message Access Protocol)

### Port

```
143
```

### Purpose

Access email stored on server.

### Difference from POP3

|POP3|IMAP|
|---|---|
|Downloads mail|Syncs mail|
|Local storage|Server storage|

---

# Network Management Protocols

## SNMP (Simple Network Management Protocol)

### Port

```
161
```

### Purpose

Monitoring network devices.

Used by:

- Routers
    
- Switches
    
- Servers
    

---

## NTP (Network Time Protocol)

### Port

```
123
```

### Purpose

Synchronizes time across devices.

Example:

```
ntpdate pool.ntp.org
```

---

# Routing Protocols

## RIP (Routing Information Protocol)

### Port

```
520
```

### Purpose

Dynamic routing protocol.

### Working

Routers exchange routing tables periodically.

---

## BGP (Border Gateway Protocol)

### Port

```
179
```

### Purpose

Internet backbone routing protocol.

Used by ISPs.

---

# Directory Protocol

## LDAP (Lightweight Directory Access Protocol)

### Port

```
389
```

### Purpose

Access and manage directory services.

Used in:

- Active Directory
    
- Enterprise authentication
    

---

# VPN Protocols

## IPSec

### Purpose

Secure IP communications using encryption.

Used in:

- VPN connections
    

---

# Messaging Protocol

## MQTT

### Port

```
1883
```

### Purpose

Lightweight messaging protocol.

Used in:

- IoT devices
    
- Sensors
    

---

# Database Protocols

|Port|Database|
|---|---|
|3306|MySQL|
|5432|PostgreSQL|
|1433|MS SQL|
|27017|MongoDB|

---

# Cybersecurity Importance

Understanding protocols helps in:

- Network scanning
    
- Packet analysis
    
- Exploiting vulnerabilities
    
- Detecting attacks
    

Example:

```
nmap -sV target
```

Shows running protocols.

---

# Summary

|Protocol|Use|
|---|---|
|TCP|Reliable communication|
|UDP|Fast communication|
|IP|Addressing|
|ICMP|Network diagnostics|
|ARP|IP to MAC mapping|
|FTP|File transfer|
|SSH|Secure remote access|
|SMTP|Sending emails|
|POP3|Email retrieval|
|IMAP|Email access|
|SNMP|Network monitoring|
|NTP|Time synchronization|
|BGP|Internet routing|
|LDAP|Directory services|
|MQTT|IoT messaging|

---