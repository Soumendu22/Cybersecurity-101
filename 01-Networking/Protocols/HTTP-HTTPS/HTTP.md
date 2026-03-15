# HTTP (HyperText Transfer Protocol)

## Overview

**HTTP** is an application layer protocol used for communication between web browsers and web servers.

It is the foundation of **data communication on the World Wide Web**.

HTTP works on a **request-response model**.

---

# Default Port

|Protocol|Port|
|---|---|
|HTTP|80|

---

# How HTTP Works

Flow:

```
Client (Browser) → HTTP Request → Web Server
Web Server → HTTP Response → Client
```

Example:

```
User enters: http://example.com
```

Browser sends request to server.

---

# HTTP Request Structure

|Component|Description|
|---|---|
|Request Line|Method + URL|
|Headers|Additional information|
|Body|Data sent to server|

Example request:

```
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla
```

---

# HTTP Methods

|Method|Purpose|
|---|---|
|GET|Retrieve data|
|POST|Send data|
|PUT|Update resource|
|DELETE|Remove resource|
|HEAD|Retrieve headers only|
|OPTIONS|Show allowed methods|

Example:

```
GET /login HTTP/1.1
```

---

# HTTP Response Structure

|Component|Description|
|---|---|
|Status Line|Status code|
|Headers|Server metadata|
|Body|Requested content|

Example:

```
HTTP/1.1 200 OK
Content-Type: text/html
```

---

# HTTP Status Codes

|Code|Meaning|
|---|---|
|200|Success|
|301|Redirect|
|400|Bad request|
|401|Unauthorized|
|403|Forbidden|
|404|Not found|
|500|Server error|

---

# Problems with HTTP

HTTP is **not secure**.

Issues:

- Data sent in plaintext
    
- Vulnerable to sniffing
    
- Vulnerable to MITM attacks
    

Example attack:

```
Packet capture → Credentials visible
```

---

# HTTP in Cybersecurity

Many attacks target HTTP:

|Attack|Description|
|---|---|
|SQL Injection|Database attack|
|XSS|Script injection|
|CSRF|Request forgery|
|Directory traversal|Access restricted files|

---

# Example Packet

```
GET /login HTTP/1.1
Host: example.com
Cookie: sessionid=abc123
```

Attackers can steal session cookies.

---