# Networking Tools

## Overview

Networking tools help in:

- Diagnosing network problems
    
- Performing reconnaissance
    
- Monitoring traffic
    
- Testing connectivity
    

---

# Ping

Tests connectivity between systems.

Example:

```bash
ping google.com
```

Uses **ICMP protocol**.

---

# Traceroute

Shows path packets take to reach destination.

Example:

```bash
traceroute google.com
```

---

# Netcat (nc)

Known as the **Swiss army knife of networking**.

Uses:

- Port scanning
    
- File transfer
    
- Reverse shells
    

Example:

```bash
nc -lvnp 4444
```

---

# tcpdump

Command-line packet capture tool.

Example:

```bash
tcpdump -i eth0
```

Capture HTTP traffic:

```bash
tcpdump port 80
```

---

# dig

DNS query tool.

Example:

```bash
dig google.com
```

Check name servers:

```bash
dig NS google.com
```

---

# whois

Shows domain registration details.

Example:

```bash
whois google.com
```

---

# netstat

Displays network connections.

Example:

```bash
netstat -tulnp
```

Shows listening ports.

---

# Summary

| Tool       | Purpose             |
| ---------- | ------------------- |
| ping       | Connectivity test   |
| traceroute | Route tracing       |
| netcat     | Networking utility  |
| tcpdump    | Packet capture      |
| dig        | DNS queries         |
| whois      | Domain information  |
| netstat    | Network connections |