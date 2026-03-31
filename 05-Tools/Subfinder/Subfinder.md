# Subfinder

## Overview

Subfinder is a fast passive subdomain enumeration tool using multiple data sources.

---

## Basic Usage

```bash
subfinder -d example.com
```

Save output:

```bash
subfinder -d example.com -o subdomains.txt
```

---

## Useful Options

- `-silent`: cleaner output for pipelines
- `-all`: use all available sources
- `-recursive`: recursive subdomain discovery where supported
- `-dL`: domain list input

Examples:

```bash
subfinder -d example.com -silent
subfinder -dL domains.txt -o all-subs.txt
```

---

## Pipeline Integration

Combine with DNS resolution and HTTP probing:

```bash
subfinder -d example.com -silent | sort -u | tee subs.txt
cat subs.txt | httpx -silent -title -status-code
```

---

## Quality and Validation

Passive results can contain stale data.

Always validate:

- DNS resolution
- active HTTP services
- scope relevance

---

## Workflow

1. Passive discovery with Subfinder.
2. Deduplicate results.
3. Resolve and probe live hosts.
4. Feed live hosts into web scanning tools.
5. Track newly discovered assets over time.

---

## Practice Tasks

1. Enumerate subdomains for a lab domain.
2. Validate live hosts with HTTP probing.
3. Compare Subfinder results with Amass passive mode.
4. Build automated recon pipeline for daily runs.
5. Record new asset findings for attack surface tracking.
