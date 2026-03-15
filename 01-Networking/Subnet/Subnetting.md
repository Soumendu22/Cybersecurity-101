# Subnetting

## Overview

Subnetting is the process of dividing a large network into **smaller logical networks (subnets)**.

It improves:

- Network organization
    
- Security
    
- Performance
    
- IP address management
    

Example:

Instead of one large network:

```
192.168.1.0/24
```

It can be divided into smaller subnets.

---

# Why Subnetting is Used

Subnetting helps in:

|Purpose|Explanation|
|---|---|
|Network segmentation|Divide networks logically|
|Security|Limit attack spread|
|Efficient IP use|Reduce wasted addresses|
|Traffic control|Reduce broadcast traffic|

Example:

```
Department networks
192.168.1.0 → HR
192.168.2.0 → Finance
192.168.3.0 → IT
```

---

# IP Address Structure

IPv4 address:

```
192.168.1.10
```

Consists of **32 bits**.

Split into:

|Part|Purpose|
|---|---|
|Network ID|Identifies network|
|Host ID|Identifies device|

Example:

```
192.168.1.10
```

Network → 192.168.1  
Host → 10

---

# Subnet Mask

A **subnet mask** separates network and host portions of an IP.

Example:

```
255.255.255.0
```

Binary:

```
11111111.11111111.11111111.00000000
```

Network bits → 24  
Host bits → 8

---

# CIDR Notation

CIDR simplifies subnet representation.

Example:

```
192.168.1.0/24
```

Meaning:

|Part|Meaning|
|---|---|
|192.168.1.0|Network|
|/24|Network bits|

---

# Private IP Address Ranges

These are reserved for internal networks.

|Range|Class|
|---|---|
|10.0.0.0 – 10.255.255.255|Class A|
|172.16.0.0 – 172.31.255.255|Class B|
|192.168.0.0 – 192.168.255.255|Class C|

Example:

```
192.168.1.1
```

---

# Subnet Calculation Example

Network:

```
192.168.1.0/24
```

Hosts available:

```
2^8 = 256
```

Usable hosts:

```
256 - 2 = 254
```

Because:

|Address|Purpose|
|---|---|
|Network address|Identifies network|
|Broadcast address|Sends to all devices|

---

# Example Subnets

Divide:

```
192.168.1.0/24
```

Into 4 networks.

|Subnet|Range|
|---|---|
|192.168.1.0/26|0–63|
|192.168.1.64/26|64–127|
|192.168.1.128/26|128–191|
|192.168.1.192/26|192–255|

---

# Network Address

First address in subnet.

Example:

```
192.168.1.0
```

---

# Broadcast Address

Last address in subnet.

Example:

```
192.168.1.255
```

---

# Host Range

Devices use addresses between network and broadcast.

Example:

```
192.168.1.1 → 192.168.1.254
```

---

# Subnetting in Cybersecurity

Subnetting helps security teams:

|Use|Purpose|
|---|---|
|Network segmentation|Limit attacker movement|
|Firewall rules|Control access|
|Monitoring|Detect suspicious traffic|

Example:

```
Nmap scan limited to subnet
```

```
nmap 192.168.1.0/24
```

---

# Summary

|Concept|Meaning|
|---|---|
|Subnet|Smaller network|
|Subnet mask|Defines network size|
|CIDR|Simplified subnet notation|
|Broadcast|Message to all hosts|
|Network address|First IP in subnet|

---