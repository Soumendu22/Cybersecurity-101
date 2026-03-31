# Cybersecurity Tools Master Guide

## Overview

This section documents practical offensive and defensive security tools with:

- Purpose and when to use
- Installation and quick start
- High-value commands
- Workflow examples
- Detection and safety notes

Always use these tools only in authorized environments.

---

## Tool Categories

1. Reconnaissance: Subfinder, Amass, Recon workflows
2. Web Enumeration: FFUF, Dirsearch, Gobuster
3. Web Proxy and Testing: Burp Suite
4. Vulnerability Scanning: Nuclei, Nikto
5. Exploitation Frameworks: Metasploit
6. Network Analysis: Nmap, Wireshark, Tcpdump
7. Credential Attacks (authorized labs): Hydra, John the Ripper
8. Injection Automation: sqlmap

---

## General Workflow

1. Scope and authorization check
2. Passive recon first
3. Active enumeration gradually
4. Validate vulnerabilities manually
5. Exploit only where approved
6. Capture evidence and remediation guidance

---

## Output Management Best Practices

- Save structured outputs (`json`, `xml`, `gnmap`, `pcap`)
- Use timestamped directories per target
- Keep raw + cleaned reports
- Record command history used in findings

Example structure:

```bash
mkdir -p results/{recon,scan,web,exploitation,pcap,reports}
```

---

## Safety and OPSEC Notes

- Start with low-noise scans
- Respect target rate limits
- Avoid destructive flags unless approved
- Use VPN/jump infrastructure as required by engagement rules
- Protect sensitive findings and credentials

---

## Reporting Checklist

- What command was run
- Why it was run
- What evidence was collected
- Risk and impact
- Reproduction steps
- Remediation recommendation

---

## Practice Plan

1. Build a reusable recon script pipeline.
2. Run web enumeration with at least two tools and compare coverage.
3. Correlate nmap, nuclei, and manual findings into one report.
4. Capture and analyze traffic for one test scenario.
5. Create final report templates per tool category.
