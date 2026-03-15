# Network Ports

## Overview

A **port** is a logical communication endpoint used by network protocols to identify specific processes or services running on a device.

Ports work with **IP addresses** to deliver data to the correct service.

Example:

```
192.168.1.1:80
```

Here:

- **192.168.1.1 → IP Address**
    
- **80 → Port Number**
    

---

# Port Range

|Range|Type|Description|
|---|---|---|
|0 – 1023|Well Known Ports|Reserved for common services|
|1024 – 49151|Registered Ports|Used by applications|
|49152 – 65535|Dynamic / Private Ports|Temporary ports|

---

# TCP vs UDP Ports

|Feature|TCP|UDP|
|---|---|---|
|Connection|Connection oriented|Connectionless|
|Reliability|Reliable|Unreliable|
|Speed|Slower|Faster|
|Example Services|HTTP, SSH, FTP|DNS, Streaming|

---

# Common Ports

|Port|Protocol|Service|Description|
|---|---|---|---|
|20|TCP|FTP Data|File transfer data|
|21|TCP|FTP|File Transfer Protocol|
|22|TCP|SSH|Secure remote login|
|23|TCP|Telnet|Remote login (insecure)|
|25|TCP|SMTP|Email sending|
|53|TCP/UDP|DNS|Domain name resolution|
|67|UDP|DHCP|Dynamic IP allocation|
|68|UDP|DHCP|DHCP client|
|69|UDP|TFTP|Trivial file transfer|
|80|TCP|HTTP|Web traffic|
|110|TCP|POP3|Email retrieval|
|119|TCP|NNTP|Network news|
|123|UDP|NTP|Time synchronization|
|137|UDP|NetBIOS|Name service|
|138|UDP|NetBIOS|Datagram service|
|139|TCP|NetBIOS|Session service|
|143|TCP|IMAP|Email retrieval|
|161|UDP|SNMP|Network monitoring|
|179|TCP|BGP|Routing protocol|
|389|TCP/UDP|LDAP|Directory services|
|443|TCP|HTTPS|Secure web traffic|
|445|TCP|SMB|File sharing|
|465|TCP|SMTPS|Secure SMTP|
|500|UDP|ISAKMP|VPN key exchange|
|514|UDP|Syslog|System logging|
|515|TCP|LPD|Printer service|
|520|UDP|RIP|Routing protocol|
|587|TCP|SMTP|Email submission|
|636|TCP|LDAPS|Secure LDAP|
|989|TCP|FTPS|Secure FTP|
|990|TCP|FTPS|Secure FTP control|
|993|TCP|IMAPS|Secure IMAP|
|995|TCP|POP3S|Secure POP3|
|1433|TCP|MSSQL|Microsoft SQL|
|1521|TCP|Oracle DB|Oracle database|
|2049|TCP|NFS|Network file system|
|2082|TCP|cPanel|Web hosting panel|
|2083|TCP|cPanel SSL|Secure cPanel|
|2181|TCP|Zookeeper|Coordination service|
|2375|TCP|Docker|Docker API|
|2483|TCP|Oracle|Secure Oracle|
|2484|TCP|Oracle|Secure Oracle|
|3000|TCP|Dev Server|Development apps|
|3306|TCP|MySQL|Database|
|3389|TCP|RDP|Remote desktop|
|3690|TCP|Subversion|Version control|
|4444|TCP|Metasploit|Reverse shells|
|4567|TCP|Sinatra|Ruby web framework|
|5000|TCP|Flask|Python server|
|5432|TCP|PostgreSQL|Database|
|5601|TCP|Kibana|Logging dashboard|
|5900|TCP|VNC|Remote desktop|
|5985|TCP|WinRM|Windows remote mgmt|
|5986|TCP|WinRM HTTPS|Secure WinRM|
|6379|TCP|Redis|In-memory database|
|6443|TCP|Kubernetes API|Container orchestration|
|6667|TCP|IRC|Chat server|
|7001|TCP|WebLogic|Oracle server|
|7002|TCP|WebLogic SSL|Secure WebLogic|
|8000|TCP|HTTP Alt|Web services|
|8008|TCP|HTTP Proxy|Proxy server|
|8080|TCP|HTTP Alt|Web server|
|8081|TCP|HTTP Alt|Dev server|
|8443|TCP|HTTPS Alt|Secure web|
|9000|TCP|SonarQube|Code analysis|
|9042|TCP|Cassandra|Database|
|9092|TCP|Kafka|Messaging system|
|9200|TCP|Elasticsearch|Search engine|
|9418|TCP|Git|Version control|
|27017|TCP|MongoDB|Database|

---

# Ports in Cybersecurity

Ports help attackers identify **running services**.

Example scan:

```
nmap -p- target
```

Example output:

```
22/tcp open ssh
80/tcp open http
443/tcp open https
```

---

# Important Attack Targets

|Port|Attack Example|
|---|---|
|21|FTP brute force|
|22|SSH brute force|
|23|Telnet credential attack|
|80|Web vulnerabilities|
|443|Web vulnerabilities|
|445|SMB exploits|
|3389|RDP brute force|

---

# Firewall Concept

Firewalls control which ports are open.

Example:

```
Allow: 80,443
Block: 23
```

---

# Quick Summary

|Concept|Meaning|
|---|---|
|Port|Communication endpoint|
|IP + Port|Identifies service|
|Open port|Service running|
|Closed port|No service|

Example:

```
192.168.1.5:22 → SSH
```