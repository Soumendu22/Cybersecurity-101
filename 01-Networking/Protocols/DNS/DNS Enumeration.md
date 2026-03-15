# DNS Enumeration

## Overview

**DNS Enumeration** is the process of gathering information about a domain using the **Domain Name System**.

It helps identify:

- Subdomains
    
- IP addresses
    
- Mail servers
    
- Name servers
    
- DNS records
    

This is a **reconnaissance technique used in penetration testing**.

---

# Why DNS Enumeration is Important

Attackers use DNS enumeration to:

- Discover hidden subdomains
    
- Identify infrastructure
    
- Find attack surfaces
    
- Map company networks
    

Example:

```
example.com
mail.example.com
vpn.example.com
dev.example.com
```

---

# DNS Record Types

|Record|Purpose|
|---|---|
|A|Maps domain to IPv4|
|AAAA|Maps domain to IPv6|
|MX|Mail server|
|NS|Name server|
|CNAME|Domain alias|
|TXT|Verification or metadata|
|PTR|Reverse DNS lookup|

Example:

```
example.com → A → 192.168.1.10
```

---

# DNS Enumeration Techniques

## 1 Subdomain Enumeration

Discover hidden subdomains.

Example:

```
dev.example.com
api.example.com
admin.example.com
```

Tools used:

- Subfinder
    
- Amass
    
- Assetfinder
    

Example command:

```
subfinder -d example.com
```

---

## 2 DNS Zone Transfer

A **zone transfer** allows replication of DNS records between servers.

If misconfigured, attackers can download **all DNS records**.

Example command:

```
dig axfr example.com @ns1.example.com
```

Successful output may reveal:

```
mail.example.com
vpn.example.com
dev.example.com
```

---

## 3 Reverse DNS Lookup

Find domains associated with an IP.

Command:

```
dig -x 8.8.8.8
```

or

```
nslookup 8.8.8.8
```

---

## 4 Brute Force Subdomain Discovery

Try common subdomain names.

Example tool:

```
ffuf
```

Example command:

```
ffuf -u https://FUZZ.example.com -w subdomains.txt
```

---

# DNS Enumeration Tools

|Tool|Purpose|
|---|---|
|dig|DNS query tool|
|nslookup|Query DNS servers|
|host|Simple DNS lookup|
|subfinder|Subdomain discovery|
|amass|Attack surface mapping|
|dnsrecon|DNS enumeration|
|dnsenum|DNS information gathering|

---

# Important DNS Commands

### dig

```
dig example.com
```

Query MX records:

```
dig MX example.com
```

Query name servers:

```
dig NS example.com
```

---

### nslookup

```
nslookup example.com
```

---

### host

```
host example.com
```

---

# Example DNS Enumeration Workflow

Step 1:

```
subfinder -d example.com
```

Step 2:

```
dig NS example.com
```

Step 3:

```
dig axfr example.com @ns1.example.com
```

Step 4:

```
dnsrecon -d example.com
```

---

# DNS Enumeration in Cybersecurity

Used in:

- Bug bounty
    
- Red team operations
    
- Penetration testing
    
- OSINT investigations
    

---

# Security Risks

Misconfigured DNS can lead to:

|Issue|Impact|
|---|---|
|Zone transfer enabled|Full domain exposure|
|Subdomain takeover|Domain hijacking|
|DNS spoofing|Traffic redirection|
|DNS tunneling|Data exfiltration|

---

# Summary

|Concept|Meaning|
|---|---|
|DNS enumeration|Information gathering|
|Subdomain discovery|Finding hidden services|
|Zone transfer|DNS database replication|
|Reverse lookup|IP → Domain|