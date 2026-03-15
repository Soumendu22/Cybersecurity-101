# Nmap (Network Mapper)

## Overview

**Nmap (Network Mapper)** is an open-source tool used for **network discovery and security auditing**.

It is widely used by:

- Penetration testers
    
- System administrators
    
- Security researchers

### Main Uses

- Discover hosts on a network
    
- Scan open ports
    
- Detect services and versions
    
- Identify operating systems
    
- Find vulnerabilities

---

# Basic Syntax

```bash
nmap [Scan Type] [Options] {target}
```

Example:

```bash
nmap 192.168.1.1
```

---

# Target Specification

|Command|Description|
|---|---|
|`nmap 192.168.1.1`|Scan single host|
|`nmap 192.168.1.1 192.168.1.2`|Scan multiple hosts|
|`nmap 192.168.1.1-100`|Scan range of IPs|
|`nmap 192.168.1.0/24`|Scan subnet|
|`nmap scanme.nmap.org`|Scan domain|
|`nmap -iL targets.txt`|Scan from file|

---

# Port Scanning Techniques

|Command|Scan Type|Description|
|---|---|---|
|`nmap -sS target`|SYN Scan|Half-open stealth scan|
|`nmap -sT target`|TCP Connect|Full TCP connection|
|`nmap -sU target`|UDP Scan|Scan UDP ports|
|`nmap -sA target`|ACK Scan|Firewall rule discovery|
|`nmap -sN target`|NULL Scan|No flags set|
|`nmap -sF target`|FIN Scan|FIN flag scan|
|`nmap -sX target`|Xmas Scan|FIN, PSH, URG flags|

---

# Host Discovery

|Command|Description|
|---|---|
|`nmap -sn 192.168.1.0/24`|Ping scan (host discovery only)|
|`nmap -Pn target`|Skip host discovery|
|`nmap -PS target`|TCP SYN ping|
|`nmap -PA target`|TCP ACK ping|
|`nmap -PU target`|UDP ping|

---

# Port Specification

|Command|Description|
|---|---|
|`nmap -p 80 target`|Scan port 80|
|`nmap -p 1-1000 target`|Scan ports 1-1000|
|`nmap -p- target`|Scan all 65535 ports|
|`nmap -F target`|Fast scan (top ports)|
|`nmap --top-ports 100 target`|Scan top 100 ports|

---

# Service and Version Detection

|Command|Description|
|---|---|
|`nmap -sV target`|Detect service versions|
|`nmap -sV --version-intensity 5 target`|Control version detection|

Example:

```bash
nmap -sV 192.168.1.1
```

Output Example:

```
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41
22/tcp open  ssh     OpenSSH 8.2
```

---

# Operating System Detection

|Command|Description|
|---|---|
|`nmap -O target`|Detect OS|
|`nmap -A target`|Aggressive scan|

Example:

```bash
nmap -O 192.168.1.1
```

---

# Aggressive Scan

```bash
nmap -A target
```

Performs:

- OS detection
    
- Version detection
    
- Script scanning
    
- Traceroute

---

# Nmap Scripting Engine (NSE)

Nmap has **hundreds of scripts for vulnerability scanning**.

|Command|Description|
|---|---|
|`nmap --script=vuln target`|Run vulnerability scripts|
|`nmap --script=http-enum target`|Enumerate web directories|
|`nmap --script=ftp-anon target`|Check anonymous FTP|
|`nmap --script=smb-os-discovery target`|SMB OS discovery|

Example:

```bash
nmap --script=vuln 192.168.1.1
```

---

# Timing and Performance

|Command|Description|
|---|---|
|`nmap -T0`|Paranoid|
|`nmap -T1`|Sneaky|
|`nmap -T2`|Polite|
|`nmap -T3`|Normal|
|`nmap -T4`|Aggressive|
|`nmap -T5`|Insane|

Example:

```bash
nmap -T4 target
```

---

# Output Options

|Command|Description|
|---|---|
|`nmap -oN scan.txt target`|Normal output|
|`nmap -oX scan.xml target`|XML output|
|`nmap -oG scan.gnmap target`|Grepable output|
|`nmap -oA scan target`|All formats|

Example:

```bash
nmap -oA scan_results 192.168.1.1
```

---

# Useful Practical Scans

### Basic Scan

```bash
nmap target
```

### Scan Specific Ports

```bash
nmap -p 80,443 target
```

### Service Detection

```bash
nmap -sV target
```

### Aggressive Scan

```bash
nmap -A target
```

### Full Port Scan

```bash
nmap -p- target
```

### Stealth Scan

```bash
nmap -sS target
```

### Vulnerability Scan

```bash
nmap --script vuln target
```

---

# Real World Pentesting Workflow

Typical pentester scan:

```bash
nmap -sC -sV -p- -T4 target
```

Explanation:

| Option | Meaning           |
| ------ |:----------------- |
| `-sC`  | Default scripts   |
| `-sV`  | Version detection |
| `-p-`  | Scan all ports    |
| `-T4`  | Faster scan       |

---

# Common Ports Reference

|Port|Service|
|---|---|
|21|FTP|
|22|SSH|
|23|Telnet|
|25|SMTP|
|53|DNS|
|80|HTTP|
|110|POP3|
|139|NetBIOS|
|143|IMAP|
|443|HTTPS|
|445|SMB|
|3306|MySQL|
|3389|RDP|

---

# Example Scan

```bash
nmap -A scanme.nmap.org
```

Example Output:

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH
80/tcp open  http    Apache
```

---

# Important Notes

- Always scan **systems you have permission to test**
    
- Unauthorized scanning may be illegal
    
- Use Nmap responsibly
    

---

# References

Official Website:  
[https://nmap.org](https://nmap.org)

Documentation:  
[https://nmap.org/docs.html](https://nmap.org/docs.html)