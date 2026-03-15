# DNS (Domain Name System)

## Overview

DNS translates **domain names into IP addresses**.

Example:

```
google.com → 142.250.190.78
```

Without DNS users would need to remember IP addresses.

---

# Default Port

|Protocol|Port|
|---|---|
|DNS|53 (UDP/TCP)|

---

# How DNS Works

DNS resolution process:

```
User → DNS Resolver → Root Server
Root Server → TLD Server
TLD Server → Authoritative Server
Authoritative Server → IP Address
```

Example:

```
User types: google.com
DNS returns: 142.250.190.78
```

---

# DNS Record Types

|Record|Purpose|
|---|---|
|A|Domain to IPv4|
|AAAA|Domain to IPv6|
|MX|Mail servers|
|CNAME|Domain alias|
|NS|Name server|
|TXT|Verification records|

Example:

```
example.com → A → 192.168.1.1
```

---

# DNS Components

|Component|Role|
|---|---|
|Resolver|Handles user query|
|Root server|Top level DNS|
|TLD server|Domain extension server|
|Authoritative server|Final IP source|

---

# DNS Query Types

|Type|Description|
|---|---|
|Recursive|Resolver finds answer|
|Iterative|Resolver queries servers step-by-step|

---

# DNS Cache

DNS responses are cached to speed up queries.

Example:

```
Browser cache
OS cache
DNS resolver cache
```

---

# DNS in Cybersecurity

DNS is heavily abused by attackers.

|Attack|Description|
|---|---|
|DNS Spoofing|Fake DNS responses|
|DNS Tunneling|Data exfiltration|
|DNS Amplification|DDoS attack|
|Domain hijacking|Takeover domain|

Example malicious query:

```
data.attacker.com
```

---

# Example DNS Lookup

Command:

```
nslookup google.com
```

Output:

```
Server: 8.8.8.8
Address: 142.250.190.78
```

---