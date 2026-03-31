# John the Ripper

## Overview

John the Ripper is a password cracking tool for offline hash analysis in incident response and authorized security testing.

---

## Basic Usage

```bash
john hashes.txt
```

Use a custom wordlist:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

Show cracked passwords:

```bash
john --show hashes.txt
```

---

## Common Modes

- Single mode (fast heuristics)
- Wordlist mode
- Incremental/brute-force mode
- Rules-based mutations

Rules example:

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

---

## Hash Identification

Use helper tools to identify hash type before cracking.

```bash
hashid '<hash-value>'
```

---

## Performance and Strategy

- Start with likely passwords/wordlists first
- Use rules before full brute-force
- Prioritize high-value account hashes
- Track cracking time and hit rates

---

## Security and IR Use Cases

- Validate password policy strength
- Assess impact of hash dumps
- Identify reused weak credentials
- Support credential hygiene remediation

---

## Practice Tasks

1. Crack sample hashes in a lab using wordlist mode.
2. Compare rule-based and incremental performance.
3. Build custom targeted wordlist from OSINT hints.
4. Measure password policy weakness from crack results.
5. Create remediation recommendations based on findings.
