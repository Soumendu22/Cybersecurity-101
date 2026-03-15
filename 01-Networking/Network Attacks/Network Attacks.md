# Network Attacks

## Overview

Network attacks target communication between systems.

Attackers attempt to:

- Intercept traffic
    
- Modify packets
    
- Disrupt communication
    
- Gain unauthorized access
    

These attacks occur at different networking layers.

---

# Man-in-the-Middle (MITM)

## Description

A **MITM attack** occurs when an attacker secretly intercepts communication between two parties.

Example:

```text
User → Attacker → Server
```

Instead of:

```text
User → Server
```

## Common Techniques

|Technique|Description|
|---|---|
|ARP spoofing|Redirect traffic|
|DNS spoofing|Fake DNS responses|
|SSL stripping|Downgrade HTTPS|

---

# ARP Poisoning

## Description

Attacker sends fake ARP messages to associate their MAC address with another IP.

Example:

```text
Gateway IP → Attacker MAC
```

Victim sends traffic to attacker.

## Tools

- ettercap
    
- arpspoof
    
- bettercap
    

---

# DNS Spoofing

## Description

Attacker sends fake DNS responses.

Example:

```text
google.com → attacker server
```

Victim is redirected to malicious site.

---

# Packet Sniffing

## Description

Capturing network traffic to read data.

Example tools:

- Wireshark
    
- tcpdump
    

Risk:

Credentials may be visible in plaintext.

---

# SYN Flood Attack

## Description

A type of **DoS attack** targeting TCP handshake.

Attacker sends many SYN packets but never completes handshake.

Example:

```text
SYN → Server
SYN → Server
SYN → Server
```

Server resources become exhausted.

---

# DNS Amplification Attack

## Description

A **DDoS attack** using DNS servers.

Attacker sends small request but causes large response.

Effect:

Target receives massive traffic.

---

# Password Attacks

Attackers target network services.

|Service|Attack|
|---|---|
|SSH|Brute force|
|FTP|Credential guessing|
|SMB|Password spraying|

---

# Summary

| Attack          | Target                     |
| --------------- | -------------------------- |
| MITM            | Communication interception |
| ARP poisoning   | Local network              |
| DNS spoofing    | Domain resolution          |
| SYN flood       | TCP connections            |
| Packet sniffing | Network traffic            |