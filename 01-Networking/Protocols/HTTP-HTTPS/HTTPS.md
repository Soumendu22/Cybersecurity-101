# HTTPS (HyperText Transfer Protocol Secure)

## Overview

**HTTPS** is the secure version of HTTP.

It uses **TLS/SSL encryption** to protect communication between client and server.

---

# Default Port

|Protocol|Port|
|---|---|
|HTTPS|443|

---

# Why HTTPS is Used

HTTPS protects:

- Login credentials
    
- Credit card information
    
- Personal data
    

It prevents:

- Packet sniffing
    
- Man-in-the-middle attacks
    
- Data tampering
    

---

# How HTTPS Works

HTTPS =

```
HTTP + TLS Encryption
```

Flow:

```
Client → TLS Handshake → Secure Channel
Client → Encrypted HTTP Request
Server → Encrypted Response
```

---

# TLS Handshake

Steps:

1. Client hello
    
2. Server hello
    
3. Certificate exchange
    
4. Key generation
    
5. Secure communication
    

Example:

```
Client → Hello
Server → Certificate
Client → Verify certificate
Secure channel established
```

---

# Digital Certificates

HTTPS uses **X.509 certificates**.

Certificate contains:

|Field|Description|
|---|---|
|Domain name|Website identity|
|Public key|Encryption key|
|Issuer|Certificate authority|
|Validity|Expiration dates|

Certificate authorities:

- Let's Encrypt
    
- DigiCert
    
- GlobalSign
    

---

# Encryption Process

Encryption uses:

- Symmetric encryption
    
- Asymmetric encryption
    

Process:

```
Public key → Encrypt
Private key → Decrypt
```

---

# HTTPS Security Features

|Feature|Benefit|
|---|---|
|Encryption|Protects data|
|Authentication|Verifies server|
|Integrity|Prevents tampering|

---

# HTTPS in Cybersecurity

Common attacks:

|Attack|Description|
|---|---|
|SSL stripping|Downgrade attack|
|Certificate spoofing|Fake certificates|
|TLS vulnerabilities|Weak encryption|

---

# Example Secure Request

```
https://example.com/login
```

Browser shows **lock icon 🔒** indicating encrypted connection.

---