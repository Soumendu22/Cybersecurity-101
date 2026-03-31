# Hydra

## Overview

Hydra is a parallelized login brute-force tool supporting many protocols (SSH, FTP, HTTP forms, RDP, SMB, and more).

Use only in explicitly authorized testing environments.

---

## Basic Usage

Single user + password list:

```bash
hydra -l admin -P passwords.txt ssh://10.10.10.10
```

User list + password list:

```bash
hydra -L users.txt -P passwords.txt ssh://10.10.10.10
```

---

## HTTP Form Example

```bash
hydra -L users.txt -P passwords.txt target.local http-post-form "/login:username=^USER^&password=^PASS^:F=Invalid"
```

Define failure/success indicators carefully to reduce false positives.

---

## Useful Options

- `-t`: parallel tasks
- `-f`: stop after first valid result
- `-s`: custom port
- `-V`: verbose attempt output
- `-o`: output file

Example:

```bash
hydra -L users.txt -P pass.txt -t 4 -f -o hydra-results.txt ssh://10.10.10.10
```

---

## Safety and Ethics

- Rate-limit attempts to avoid service disruption
- Follow lockout policy constraints in tests
- Coordinate brute-force windows with defenders
- Never run against unauthorized targets

---

## Practice Tasks

1. Test SSH credential spraying in a lab VM.
2. Build accurate HTTP form module syntax for test app.
3. Tune thread count to balance speed and noise.
4. Validate discovered credentials safely.
5. Document lockout and monitoring behavior observed.
