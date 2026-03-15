# Wireshark

## Overview

**Wireshark** is one of the most powerful **network protocol analyzers** used to capture and analyze network traffic in real time.

It allows security analysts to inspect packets moving across a network.

Used in:

- Network troubleshooting
    
- Cybersecurity analysis
    
- Malware investigation
    
- Incident response
    
- Digital forensics
    

---

# Key Features

|Feature|Description|
|---|---|
|Packet capture|Captures network traffic|
|Protocol analysis|Supports hundreds of protocols|
|Deep inspection|Inspect packet details|
|Filters|Advanced packet filtering|
|Visualization|Graphical interface|

---

# Supported Platforms

Wireshark runs on:

- Linux
    
- Windows
    
- macOS
    

---

# Packet Capture Process

Steps:

1. Select network interface
    
2. Start packet capture
    
3. Filter packets
    
4. Analyze packet details
    

Example workflow:

```text
Network Traffic → Packet Capture → Packet Filtering → Packet Analysis
```

---

# Interface Components

Wireshark interface consists of:

|Section|Purpose|
|---|---|
|Packet List|Displays captured packets|
|Packet Details|Shows protocol layers|
|Packet Bytes|Raw hexadecimal data|

---

# Protocol Layers in Wireshark

When inspecting packets, Wireshark shows protocol layers.

Example:

```text
Ethernet
Internet Protocol (IP)
Transmission Control Protocol (TCP)
HTTP
```

---

# Packet Capture Filters

Capture filters limit packets captured.

Example filters:

|Filter|Description|
|---|---|
|host 192.168.1.1|Capture specific host|
|port 80|Capture HTTP traffic|
|tcp|Capture TCP packets|
|udp|Capture UDP packets|

Example:

```bash
tcp port 80
```

---

# Display Filters

Display filters analyze captured packets.

|Filter|Purpose|
|---|---|
|ip.addr == 192.168.1.1|Filter IP|
|tcp.port == 80|Filter HTTP|
|dns|Show DNS packets|
|http|Show HTTP traffic|
|tcp|Show TCP packets|

Example:

```text
tcp.port == 443
```

---

# Important Protocols in Wireshark

|Protocol|Use|
|---|---|
|TCP|Reliable communication|
|UDP|Fast communication|
|DNS|Domain resolution|
|HTTP|Web traffic|
|HTTPS|Secure web traffic|
|ICMP|Network diagnostics|
|ARP|IP to MAC mapping|

---

# Following TCP Streams

Wireshark allows reconstruction of TCP sessions.

Steps:

1 Right-click packet  
2 Select:

```text
Follow → TCP Stream
```

This shows the entire communication session.

---

# Example Packet Analysis

Captured packet example:

```text
Source IP → 192.168.1.10
Destination IP → 192.168.1.1
Protocol → TCP
Port → 443
```

Packet layers:

```text
Ethernet Frame
IP Packet
TCP Segment
TLS Data
```

---

# Detecting Attacks with Wireshark

Wireshark can help detect:

|Attack|Indicator|
|---|---|
|Port scanning|Multiple SYN packets|
|DNS tunneling|Unusual DNS traffic|
|Malware traffic|Suspicious domains|
|Data exfiltration|Large outbound traffic|

Example suspicious traffic:

```text
tcp.port == 4444
```

May indicate reverse shell.

---

# Exporting Packets

Wireshark can export packet captures.

File formats:

|Format|Description|
|---|---|
|PCAP|Packet capture|
|PCAPNG|Extended capture format|

Example file:

```text
capture.pcap
```

---

# Useful Wireshark Shortcuts

|Shortcut|Function|
|---|---|
|Ctrl + E|Start/Stop capture|
|Ctrl + F|Search packets|
|Ctrl + Shift + F|Advanced search|

---

# Wireshark in Cybersecurity

Wireshark is used in:

- Network monitoring
    
- Malware analysis
    
- Incident response
    
- Penetration testing
    
- Digital forensics
    

---

# Example Investigation Workflow

1 Capture packets  
2 Identify suspicious traffic  
3 Apply filters  
4 Analyze communication

Example filter:

```text
ip.addr == 192.168.1.5
```

---

# Summary

|Concept|Meaning|
|---|---|
|Wireshark|Packet analyzer|
|Packet capture|Recording traffic|
|Display filters|Analyze packets|
|TCP stream|Reconstruct sessions|

---