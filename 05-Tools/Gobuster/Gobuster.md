# Gobuster

## Overview

Gobuster performs brute-force discovery for web paths, DNS subdomains, and virtual hosts.

---

## Directory Mode

```bash
gobuster dir -u http://target.local -w /usr/share/wordlists/dirb/common.txt
```

Extensions:

```bash
gobuster dir -u http://target.local -w wordlist.txt -x php,txt,bak
```

---

## DNS Mode

```bash
gobuster dns -d example.com -w subdomains.txt
```

---

## VHost Mode

```bash
gobuster vhost -u http://target.local -w subdomains.txt
```

---

## Useful Flags

- `-t`: threads
- `-s`: positive status codes
- `-b`: blacklist status codes
- `-k`: skip TLS verification (lab use)
- `--delay`: control request pacing

---

## Workflow Tips

- Start with moderate thread count
- Filter known wildcard responses
- Validate discovered paths manually
- Compare output with FFUF/Dirsearch for coverage gaps

---

## Practice Tasks

1. Run directory discovery on a lab app.
2. Enumerate subdomains in DNS mode.
3. Test VHost mode on wildcard domain setup.
4. Tune threads and measure scan reliability.
5. Build merged report with FFUF and Dirsearch findings.
