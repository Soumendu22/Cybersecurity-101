# Recon Tooling Workflow

## Overview

Reconnaissance combines multiple tools and data sources to map target attack surface before testing vulnerabilities.

---

## Recon Phases

1. Passive reconnaissance (OSINT, subdomain intelligence)
2. Active reconnaissance (DNS resolution, probing, scanning)
3. Service and technology fingerprinting
4. Prioritized target selection

---

## Example Recon Pipeline

```bash
subfinder -d target.com -silent | sort -u > subs.txt
cat subs.txt | dnsx -silent > resolved.txt
cat resolved.txt | httpx -silent -title -status-code -tech-detect > web.txt
nmap -iL resolved.txt -sV -oA nmap-recon
```

---

## Data Sources to Correlate

- Certificate transparency data
- Passive DNS
- Search engine indexing
- GitHub/code leaks
- Cloud asset metadata

---

## Recon Prioritization Model

Prioritize by:

- internet exposure
- authentication boundary
- business criticality
- known vulnerable technology stacks
- historical incident relevance

---

## Recon Output Organization

```bash
mkdir -p recon/{subs,resolved,http,nmap,screenshots,notes}
```

Recommended files:

- `subs.txt`
- `resolved.txt`
- `live-http.txt`
- `nmap.xml`
- `findings.md`

---

## Recon Quality Checks

- remove duplicates and wildcard noise
- verify scope ownership
- confirm service liveness
- annotate false positives early

---

## Practice Tasks

1. Build full recon pipeline for one lab domain.
2. Identify top 10 highest-priority assets from findings.
3. Correlate web tech stack with potential vulnerability classes.
4. Automate recon output foldering and naming.
5. Produce recon summary brief for test planning.
