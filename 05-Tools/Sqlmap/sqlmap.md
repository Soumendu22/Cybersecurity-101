# sqlmap

## Overview

sqlmap automates SQL injection detection and exploitation for authorized testing. It supports multiple DBMS engines and advanced enumeration options.

---

## Basic Usage

```bash
sqlmap -u "http://target.local/item.php?id=1"
```

POST request testing:

```bash
sqlmap -u "http://target.local/login" --data="username=test&password=test"
```

---

## Common Flags

- `--batch`: non-interactive mode
- `--dbs`: enumerate databases
- `--tables -D <db>`: list tables
- `--columns -D <db> -T <table>`: list columns
- `--dump -D <db> -T <table>`: dump table data
- `--risk` and `--level`: test depth
- `--threads`: parallelism

---

## Cookie and Authenticated Testing

```bash
sqlmap -u "http://target.local/profile?id=1" --cookie="PHPSESSID=..."
```

Use authenticated context for realistic attack surface.

---

## Request File Mode (recommended)

Capture a full request in Burp and save as `req.txt`:

```bash
sqlmap -r req.txt --batch
```

This improves reproducibility and accuracy on complex endpoints.

---

## Useful Advanced Options

```bash
sqlmap -r req.txt --technique=BEUSTQ
sqlmap -r req.txt --tamper=space2comment
sqlmap -r req.txt --random-agent
sqlmap -r req.txt --flush-session
```

Use tamper scripts and deeper techniques only when permitted.

---

## Output and Evidence

sqlmap stores output under local project directories.

Best practice:

- keep command used
- keep request file
- keep output snippets proving exploitability
- validate manually before reporting critical impact

---

## Limitations

- False positives can occur
- WAFs and app logic can distort results
- Business impact still requires manual verification

---

## Safety Notes

- Avoid destructive options without written approval
- Respect production stability and rate limits
- Never dump unnecessary personal/sensitive data

---

## Practice Tasks

1. Detect SQLi on a lab GET endpoint.
2. Test authenticated endpoint with cookie/session context.
3. Use `-r` request mode from Burp for complex POST API.
4. Compare low vs high `--risk/--level` results.
5. Produce a clean vulnerability report from sqlmap evidence.
