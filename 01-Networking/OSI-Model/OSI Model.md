# OSI Model (Open Systems Interconnection Model)

## Overview

The **OSI Model** is a conceptual framework used to understand how different networking protocols interact to transmit data over a network.

It divides network communication into **7 layers**, each responsible for specific functions.

The OSI model helps in:

- Understanding network architecture
    
- Troubleshooting network issues
    
- Designing networking protocols
    
- Learning cybersecurity attacks and defenses
    

---

# The 7 Layers of OSI Model

|Layer Number|Layer Name|Main Function|
|---|---|---|
|7|Application|Provides network services to applications|
|6|Presentation|Data formatting, encryption, compression|
|5|Session|Manages sessions between devices|
|4|Transport|Reliable data transfer|
|3|Network|Routing and logical addressing|
|2|Data Link|Physical addressing and frame transmission|
|1|Physical|Transmission of raw bits over medium|

---

# Memory Trick (Mnemonic)

To remember layers from **top → bottom**

```text
All People Seem To Need Data Processing
```

|Word|Layer|
|---|---|
|All|Application|
|People|Presentation|
|Seem|Session|
|To|Transport|
|Need|Network|
|Data|Data Link|
|Processing|Physical|

---

# Layer 7 — Application Layer

## Description

The **Application Layer** provides network services directly to user applications.

This is where **users interact with the network**.

## Examples of Protocols

|Protocol|Use|
|---|---|
|HTTP|Web browsing|
|HTTPS|Secure web communication|
|FTP|File transfer|
|SMTP|Sending emails|
|POP3|Receiving emails|
|DNS|Domain name resolution|

## Example

When you open a website:

```text
Browser → HTTP → Web Server
```

Cybersecurity relevance:

- XSS
    
- SQL Injection
    
- Authentication attacks
    

---

# Layer 6 — Presentation Layer

## Description

Responsible for **data formatting, encryption, and compression**.

Ensures that data sent by one system is readable by another.

## Functions

|Function|Description|
|---|---|
|Encryption|Protects data|
|Decryption|Converts encrypted data|
|Compression|Reduces data size|
|Translation|Format conversion|

## Examples

|Technology|Use|
|---|---|
|SSL/TLS|Encryption|
|JPEG|Image format|
|MPEG|Video format|

Cybersecurity relevance:

- SSL/TLS attacks
    
- Encryption vulnerabilities
    

---

# Layer 5 — Session Layer

## Description

Manages sessions between computers.

Handles:

- Session establishment
    
- Session maintenance
    
- Session termination
    

## Functions

|Function|Description|
|---|---|
|Session creation|Start communication|
|Session management|Maintain connection|
|Session termination|End communication|

Example:

```text
User login session
```

Cybersecurity relevance:

- Session hijacking
    
- Session fixation
    

---

# Layer 4 — Transport Layer

## Description

Responsible for **end-to-end communication and data reliability**.

## Main Protocols

|Protocol|Description|
|---|---|
|TCP|Reliable communication|
|UDP|Fast but unreliable|

## TCP vs UDP

|Feature|TCP|UDP|
|---|---|---|
|Reliability|Yes|No|
|Speed|Slower|Faster|
|Connection|Connection-oriented|Connectionless|
|Use Case|Web, Email|Streaming, DNS|

## Example Ports

|Port|Protocol|Service|
|---|---|---|
|80|TCP|HTTP|
|443|TCP|HTTPS|
|53|UDP|DNS|
|22|TCP|SSH|

Cybersecurity relevance:

- Port scanning
    
- SYN flood attacks
    
- DoS attacks
    

---

# Layer 3 — Network Layer

## Description

Responsible for **routing packets between networks**.

Handles logical addressing.

## Main Protocols

|Protocol|Function|
|---|---|
|IP|Logical addressing|
|ICMP|Error reporting|
|IPSec|Secure IP communication|

## Example Devices

|Device|Function|
|---|---|
|Router|Routes packets|
|Layer 3 switch|Network routing|

Example IP:

```text
192.168.1.1
```

Cybersecurity relevance:

- IP spoofing
    
- ICMP attacks
    
- Routing attacks
    

---

# Layer 2 — Data Link Layer

## Description

Responsible for **node-to-node communication**.

Uses **MAC addresses**.

## Functions

|Function|Description|
|---|---|
|Framing|Organizing bits into frames|
|Error detection|Detect corrupted frames|
|MAC addressing|Hardware addressing|

## Protocols

|Protocol|Use|
|---|---|
|Ethernet|LAN communication|
|ARP|MAC address resolution|
|PPP|Point-to-point connection|

Example MAC address:

```text
00:1A:2B:3C:4D:5E
```

Cybersecurity relevance:

- ARP poisoning
    
- MAC spoofing
    

---

# Layer 1 — Physical Layer

## Description

Responsible for **transmitting raw bits over physical medium**.

Defines hardware specifications.

## Examples

|Component|Description|
|---|---|
|Cables|Ethernet cables|
|Fiber optics|High-speed connections|
|Switch ports|Physical interfaces|

Example transmission:

```text
010101010101
```

Cybersecurity relevance:

- Cable tapping
    
- Physical attacks
    

---

# Data Flow Through OSI Model

Example: Opening a website

```text
Application → HTTP Request
Presentation → Encryption (TLS)
Session → Session creation
Transport → TCP connection
Network → IP routing
Data Link → Frame creation
Physical → Bits transmitted
```

---

# Encapsulation Process

|Layer|Data Unit|
|---|---|
|Application|Data|
|Transport|Segment|
|Network|Packet|
|Data Link|Frame|
|Physical|Bits|

---

# Real Example (HTTP Request)

```text
User opens https://google.com
```

Flow:

```text
Application → HTTP
Presentation → TLS encryption
Session → Session established
Transport → TCP port 443
Network → IP packet
Data Link → Ethernet frame
Physical → Bits on cable
```

---

# OSI Model in Cybersecurity

Understanding OSI helps identify **where attacks occur**.

|Layer|Example Attack|
|---|---|
|Application|SQL Injection|
|Presentation|SSL attacks|
|Session|Session hijacking|
|Transport|SYN flood|
|Network|IP spoofing|
|Data Link|ARP poisoning|
|Physical|Hardware tampering|

---

# OSI vs TCP/IP Model

|OSI Layer|TCP/IP Equivalent|
|---|---|
|Application|Application|
|Presentation|Application|
|Session|Application|
|Transport|Transport|
|Network|Internet|
|Data Link|Network Access|
|Physical|Network Access|

---

# Quick Summary

|Layer|Key Idea|
|---|---|
|7|User applications|
|6|Encryption|
|5|Sessions|
|4|Reliable transport|
|3|Routing|
|2|MAC addressing|
|1|Physical transmission|

---

# References

OSI Model Documentation:  
[https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)