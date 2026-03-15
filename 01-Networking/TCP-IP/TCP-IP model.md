# TCP/IP Model (Transmission Control Protocol / Internet Protocol)

## Overview

The **TCP/IP Model** is the foundational framework used for communication on the internet.  
It defines how data is transmitted across networks using a layered approach.

Unlike the OSI model (7 layers), TCP/IP uses **4 layers**.

It was developed by **DARPA** for the ARPANET project and later became the standard for the internet.

---

# TCP/IP Layers

|Layer|Function|
|---|---|
|Application|Provides network services to applications|
|Transport|End-to-end communication|
|Internet|Logical addressing and routing|
|Network Access|Physical transmission of data|

---

# Layer Architecture

```
Application Layer
Transport Layer
Internet Layer
Network Access Layer
```

---

# Application Layer

## Purpose

The Application Layer provides network services directly to user applications.

This layer combines the **Application, Presentation, and Session layers of the OSI model**.

### Common Protocols

|Protocol|Purpose|
|---|---|
|HTTP|Web communication|
|HTTPS|Secure web traffic|
|DNS|Domain name resolution|
|FTP|File transfer|
|SMTP|Sending email|
|POP3|Email retrieval|
|IMAP|Email synchronization|
|SNMP|Network management|
|SSH|Secure remote login|

---

# Transport Layer

## Purpose

Responsible for **end-to-end communication** between hosts.

Handles:

- Data segmentation
    
- Error recovery
    
- Flow control
    
- Reliability
    

### Main Protocols

|Protocol|Description|
|---|---|
|TCP|Reliable communication|
|UDP|Fast but unreliable|

---

## TCP (Transmission Control Protocol)

### Key Features

|Feature|Description|
|---|---|
|Connection oriented|Uses handshake|
|Reliable|Guarantees delivery|
|Ordered delivery|Maintains packet order|

### TCP 3-Way Handshake

```
Client → SYN
Server → SYN-ACK
Client → ACK
```

---

## UDP (User Datagram Protocol)

### Key Features

|Feature|Description|
|---|---|
|Connectionless|No handshake|
|Faster|Low overhead|
|Unreliable|No guarantee of delivery|

Used in:

- DNS queries
    
- Video streaming
    
- Online gaming
    

---

# Internet Layer

## Purpose

Responsible for **routing packets between networks**.

This layer determines how packets travel across the internet.

### Main Protocols

|Protocol|Purpose|
|---|---|
|IP|Logical addressing|
|ICMP|Error reporting|
|ARP|IP to MAC mapping|
|IPSec|Secure IP communication|

---

## IP Addressing

Example IPv4:

```
192.168.1.1
```

Example IPv6:

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

---

# Network Access Layer

## Purpose

Handles communication with the physical network.

Responsible for:

- MAC addressing
    
- Frame transmission
    
- Physical data transmission
    

### Protocols and Technologies

|Protocol|Description|
|---|---|
|Ethernet|LAN communication|
|WiFi|Wireless networking|
|PPP|Point-to-point connections|

---

# Data Flow Through TCP/IP

Example: Opening a website.

```
Application → HTTP request
Transport → TCP segmentation
Internet → IP routing
Network Access → Frame transmission
```

---

# Encapsulation Process

When data travels through the layers, it is encapsulated.

|Layer|Data Unit|
|---|---|
|Application|Data|
|Transport|Segment|
|Internet|Packet|
|Network Access|Frame|

---

# TCP/IP vs OSI Model

|TCP/IP|OSI Equivalent|
|---|---|
|Application|Application + Presentation + Session|
|Transport|Transport|
|Internet|Network|
|Network Access|Data Link + Physical|

---

# Example Communication

User visits a website:

```
Browser → HTTP request
TCP → Port 80/443
IP → Destination address
Ethernet → Frame transmission
```

---

# TCP/IP in Cybersecurity

Understanding TCP/IP helps in:

- Network scanning
    
- Packet analysis
    
- Exploit development
    
- Network defense
    

Example reconnaissance:

```
nmap -sS target
```

This scans TCP ports.

---

# Common Attacks on TCP/IP

|Attack|Layer|
|---|---|
|SYN Flood|Transport|
|IP Spoofing|Internet|
|ARP Poisoning|Network Access|
|Session Hijacking|Application|

---

# Summary

|Layer|Role|
|---|---|
|Application|User applications|
|Transport|Reliable communication|
|Internet|Routing|
|Network Access|Physical transmission|

---