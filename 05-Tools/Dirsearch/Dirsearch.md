# Dirsearch

## Overview

Dirsearch is a web path brute-force tool for discovering hidden directories and files on web servers.

---

## Basic Usage

```bash
dirsearch -u http://target.local -w /usr/share/wordlists/dirb/common.txt
```

Multiple extensions:

```bash
dirsearch -u http://target.local -e php,asp,aspx,js,txt
```

---

## Useful Options

- `-x`: exclude status codes
- `-i`: include status codes
- `--exclude-sizes`: filter noisy result sizes
- `-t`: threads
- `--random-agent`: rotate user-agent
- `--plain-text-report`: save clean output

Example:

```bash
dirsearch -u http://target.local -e php,txt -x 400,404 -t 40
```

---

## Recursive Scanning

```bash
dirsearch -u http://target.local --recursive --deep-recursive
```

Use recursion carefully to avoid excessive requests.

---

## Authenticated Scanning

```bash
dirsearch -u http://target.local -H "Cookie: PHPSESSID=..."
```

Authenticated context often reveals admin and API routes.

---

## Workflow

1. Start with lightweight wordlist + key extensions.
2. Filter obvious noise (404 length/status).
3. Rerun with targeted list for framework-specific files.
4. Validate 200/403/401 paths manually.
5. Correlate with FFUF results.

---

## Practice Tasks

1. Enumerate hidden admin endpoints in a lab app.
2. Compare extension-based vs extensionless scans.
3. Run authenticated dirsearch and note new discoveries.
4. Build custom wordlist from app technology fingerprints.
5. Generate report with top-risk discovered paths.
