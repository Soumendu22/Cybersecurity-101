# Packet Analysis

## Overview

**Packet Analysis** is the process of capturing and inspecting network packets to understand how data travels across a network.

It is used in:

- Network troubleshooting
    
- Cybersecurity investigations
    
- Intrusion detection
    
- Malware analysis
    
- Digital forensics
    

Tools used for packet analysis include:

- Wireshark
    
- tcpdump
    
- Tshark
    
- NetworkMiner
    
- Zeek
    

---

# What is a Packet?

A **packet** is a small unit of data transmitted over a network.

Structure of a packet:

|Component|Description|
|---|---|
|Header|Contains metadata such as source and destination|
|Payload|Actual data being transmitted|

Example:

```
Source IP → 192.168.1.10
Destination IP → 8.8.8.8
Protocol → TCP
Port → 443
```

---

# Packet Structure

Packets contain multiple layers based on networking models.

|Layer|Information|
|---|---|
|Application|HTTP, DNS|
|Transport|TCP / UDP|
|Network|IP Address|
|Data Link|MAC Address|
|Physical|Bits transmitted|

---

# Key Packet Fields

|Field|Description|
|---|---|
|Source IP|Sender's IP address|
|Destination IP|Receiver's IP address|
|Source Port|Sender's port|
|Destination Port|Target service port|
|Protocol|TCP, UDP, ICMP|
|Payload|Actual transmitted data|

---

# Packet Capture Tools

|Tool|Description|
|---|---|
|Wireshark|Graphical packet analyzer|
|tcpdump|Command-line packet capture|
|Tshark|CLI version of Wireshark|
|Zeek|Network security monitoring|
|NetworkMiner|Network forensic analysis|

---

# Packet Capture Process

Steps involved:

1. Capture network traffic
    
2. Filter packets
    
3. Analyze protocols
    
4. Identify suspicious activity
    

Example workflow:

```
Network Traffic → Packet Capture → Filtering → Analysis
```

---

# tcpdump Commands

Basic packet capture:

```
tcpdump -i eth0
```

Capture specific interface:

```
tcpdump -i wlan0
```

Capture specific port:

```
tcpdump port 80
```

Capture specific IP:

```
tcpdump host 192.168.1.1
```

Save capture file:

```
tcpdump -w capture.pcap
```

---

# Wireshark Filters

Display filters allow analyzing specific traffic.

|Filter|Description|
|---|---|
|ip.addr == 192.168.1.1|Filter specific IP|
|tcp.port == 80|Filter HTTP traffic|
|dns|Show DNS packets|
|http|Show HTTP packets|
|tcp|Show TCP traffic|

Example:

```
tcp.port == 443
```

---

# Common Protocols Seen in Packet Analysis

|Protocol|Use|
|---|---|
|HTTP|Web traffic|
|HTTPS|Secure web traffic|
|DNS|Domain resolution|
|TCP|Reliable communication|
|UDP|Fast communication|
|ICMP|Network diagnostics|

---

# Suspicious Indicators in Packet Analysis

Analysts look for unusual patterns.

|Indicator|Possible Threat|
|---|---|
|High traffic|DDoS attack|
|Suspicious DNS queries|Malware communication|
|Unknown IP connections|C2 server|
|Repeated login attempts|Brute force attack|

---

# Example: DNS Packet

Example capture:

```
Source: 192.168.1.5
Destination: 8.8.8.8
Protocol: DNS
Query: google.com
```

Flow:

```
Client → DNS Query → DNS Server → Response
```

---

# Packet Analysis in Cybersecurity

Used for detecting:

|Attack|Description|
|---|---|
|DDoS|High traffic flooding|
|Data exfiltration|Data leaving network|
|Malware communication|C2 server traffic|
|DNS tunneling|Data hidden in DNS|

---

# Example Investigation

Steps:

1. Capture packets
    
2. Filter suspicious traffic
    
3. Identify attacker IP
    
4. Analyze payload
    

Example:

```
tcp.port == 4444
```

May indicate **reverse shell traffic**.

---

# Important File Formats

|Format|Description|
|---|---|
|PCAP|Packet capture format|
|PCAPNG|Extended capture format|

Example capture file:

```
capture.pcap
```

---

# Best Practices

- Capture traffic responsibly
    
- Analyze suspicious patterns
    
- Use filters to reduce noise
    
- Correlate logs with packet data
    

---

# Quick Summary

|Concept|Meaning|
|---|---|
|Packet|Unit of network data|
|Packet Capture|Recording network traffic|
|Packet Analysis|Inspecting traffic for insights|
|Tools|Wireshark, tcpdump|

---

# References

Wireshark Documentation  
[https://www.wireshark.org/docs/](https://www.wireshark.org/docs/)