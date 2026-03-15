# SMB Enumeration

## Overview

**SMB (Server Message Block)** is a protocol used for **file sharing and network resource access**.

It is widely used in **Windows networks**.

SMB allows:

- File sharing
    
- Printer sharing
    
- Remote access
    
- Inter-process communication
    

---

# Default Ports

|Port|Protocol|
|---|---|
|445|SMB|
|139|NetBIOS|

---

# Why SMB Enumeration is Important

Attackers enumerate SMB to discover:

- Shared folders
    
- User accounts
    
- Network information
    
- Domain details
    

SMB is a **common attack vector in Windows environments**.

---

# SMB Enumeration Tools

|Tool|Purpose|
|---|---|
|Nmap|Service detection|
|smbclient|Access SMB shares|
|enum4linux|SMB enumeration|
|CrackMapExec|Active directory attacks|
|smbmap|Share enumeration|

---

# Nmap SMB Enumeration

Basic scan:

```
nmap -p 445 target
```

SMB script scan:

```
nmap --script smb-enum-shares target
```

Other useful scripts:

```
nmap --script smb-os-discovery target
nmap --script smb-enum-users target
nmap --script smb-enum-domains target
```

---

# SMB Share Enumeration

List shares:

```
smbclient -L //target-ip
```

Example output:

```
ADMIN$
C$
Public
Users
```

---

# Access SMB Share

```
smbclient //target-ip/Public
```

Download file:

```
get file.txt
```

Upload file:

```
put file.txt
```

---

# enum4linux

Tool used for detailed SMB enumeration.

Command:

```
enum4linux target-ip
```

Information gathered:

- Users
    
- Shares
    
- Groups
    
- Domain info
    

---

# smbmap

Shows permissions on SMB shares.

Command:

```
smbmap -H target-ip
```

Example output:

```
Share       Permissions
Public      READ
Backup      READ/WRITE
```

---

# CrackMapExec

Powerful Active Directory tool.

Example:

```
crackmapexec smb target-ip
```

Used for:

- Password spraying
    
- Credential testing
    
- Domain enumeration
    

---

# SMB Attacks

Common attacks include:

|Attack|Description|
|---|---|
|SMB relay|Authentication relay|
|Pass-the-hash|Login using NTLM hash|
|SMB brute force|Password guessing|
|EternalBlue|SMB vulnerability exploit|

---

# SMB Enumeration Workflow

Step 1:

```
nmap -p445 target
```

Step 2:

```
smbclient -L //target-ip
```

Step 3:

```
enum4linux target-ip
```

Step 4:

```
smbmap -H target-ip
```

---

# SMB in Cybersecurity

SMB is heavily targeted in:

- Active Directory attacks
    
- Internal network pentesting
    
- Lateral movement
    

---

# Example Attack Scenario

1 Identify SMB service

```
nmap -p445 target
```

2 Enumerate shares

```
smbclient -L //target
```

3 Access public share

```
smbclient //target/Public
```

---

# Summary

|Concept|Meaning|
|---|---|
|SMB|File sharing protocol|
|Enumeration|Gathering information|
|Shares|Shared directories|
|Port|445|