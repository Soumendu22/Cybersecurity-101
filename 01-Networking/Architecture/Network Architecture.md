# Network Architecture

## Overview

**Network architecture** refers to the design and structure of a computer network.  
It defines how devices communicate, how networks are organized, and how data flows.

Network architecture includes:

- Network types (LAN, WAN, etc.)
    
- Network topologies
    
- Communication models
    
- Infrastructure design
    

Understanding network architecture is important in **cybersecurity, networking, and pentesting**.

---

# Types of Networks

Networks are categorized based on their **size and coverage area**.

---

# PAN (Personal Area Network)

## Description

A **Personal Area Network (PAN)** connects devices within a very short range around a person.

Typical range:

```text
1 – 10 meters
```

Examples:

- Bluetooth devices
    
- Smart watches
    
- Wireless headphones
    
- Phone tethering
    

Example:

```text
Smartphone → Bluetooth → Headphones
```

---

# LAN (Local Area Network)

## Description

A **Local Area Network (LAN)** connects computers within a limited geographic area.

Examples:

- Home networks
    
- Office networks
    
- School networks
    

Example:

```text
Router
  ↓
Switch
  ↓
Computers
```

Typical technologies:

- Ethernet
    
- WiFi
    

Example IP range:

```text
192.168.1.0/24
```

---

# CAN (Campus Area Network)

## Description

A **Campus Area Network (CAN)** connects multiple LANs within a campus or organization.

Examples:

- University networks
    
- Corporate campuses
    

Example:

```text
Building A LAN
Building B LAN
Building C LAN
      ↓
Campus Network
```

---

# MAN (Metropolitan Area Network)

## Description

A **Metropolitan Area Network (MAN)** spans an entire city.

Examples:

- City internet infrastructure
    
- Cable television networks
    

Example:

```text
Multiple LANs → City Network
```

---

# WAN (Wide Area Network)

## Description

A **Wide Area Network (WAN)** covers very large geographic areas.

The **Internet is the largest WAN**.

Example:

```text
Office Network → ISP → Internet
```

Technologies used:

- MPLS
    
- Satellite links
    
- Fiber optic networks
    

---

# Network Communication Models

## Client-Server Model

In this model, clients request services from servers.

Example:

```text
Client → Web Server → Response
```

Examples:

- Web browsing
    
- Email services
    
- Database servers
    

Advantages:

- Centralized control
    
- Better security
    

---

## Peer-to-Peer Model

Devices communicate directly with each other.

Example:

```text
Computer A ↔ Computer B
```

Examples:

- File sharing
    
- BitTorrent networks
    

Advantages:

- Simple
    
- No central server required
    

---

# Network Topologies

Network topology defines how devices are physically or logically connected.

---

# Bus Topology

All devices share a single communication cable.

Example:

```text
PC1 — PC2 — PC3 — PC4
```

Advantages:

- Simple design
    
- Low cost
    

Disadvantages:

- Single cable failure breaks network
    

---

# Star Topology

Devices connect to a central device such as a switch.

Example:

```text
       PC1
        |
PC2 — Switch — PC3
        |
       PC4
```

Advantages:

- Easy troubleshooting
    
- Reliable
    

Disadvantages:

- Central device failure stops network
    

---

# Ring Topology

Devices are connected in a circular structure.

Example:

```text
PC1 → PC2 → PC3 → PC4 → PC1
```

Data travels in one direction.

Disadvantages:

- One device failure breaks network
    

---

# Mesh Topology

Devices are connected with multiple paths.

Example:

```text
PC1 ↔ PC2
 ↕     ↕
PC3 ↔ PC4
```

Advantages:

- Very reliable
    
- Multiple paths
    

Disadvantages:

- Expensive
    

---

# Hybrid Topology

Combination of different topologies.

Example:

```text
Star + Mesh + Bus
```

Most modern networks use hybrid topology.

---

# Network Components

Important devices in network architecture:

|Device|Function|
|---|---|
|Router|Connect networks|
|Switch|Connect devices in LAN|
|Firewall|Protect network|
|Access Point|Provide WiFi|
|Modem|Connect to ISP|

---

# Network Segmentation

Large networks are divided into segments.

Example:

```text
HR Network
Finance Network
IT Network
```

Benefits:

- Better security
    
- Reduced traffic
    

---

# Network Architecture in Cybersecurity

Understanding architecture helps security professionals:

|Use|Purpose|
|---|---|
|Network mapping|Identify infrastructure|
|Attack surface discovery|Find exposed services|
|Segmentation|Limit attacker movement|
|Monitoring|Detect suspicious traffic|

Example reconnaissance:

```bash
nmap 192.168.1.0/24
```

---

# Summary

|Concept|Meaning|
|---|---|
|PAN|Personal network|
|LAN|Local network|
|CAN|Campus network|
|MAN|City-wide network|
|WAN|Global network|
|Topology|Network layout|
|Segmentation|Divide networks|

---