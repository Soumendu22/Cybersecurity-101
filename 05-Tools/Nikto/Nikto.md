# Nikto

## Overview

Nikto is a web server scanner for identifying common misconfigurations, outdated software, insecure files, and known dangerous defaults.

---

## Basic Scan

```bash
nikto -h http://target.local
```

SSL target:

```bash
nikto -h https://target.local
```

---

## Useful Options

- `-p`: specify port
- `-ssl`: force SSL
- `-output`: save results
- `-Format`: output format (txt, csv, html)
- `-Tuning`: select test categories

Example:

```bash
nikto -h target.local -p 8443 -ssl -output nikto.html -Format htm
```

---

## Best Use Cases

- quick baseline web misconfiguration checks
- identifying outdated server components
- finding exposed admin/debug files

Nikto findings should be validated manually for exploitability.

---

## Practice Tasks

1. Scan a lab web server and categorize findings.
2. Verify outdated software findings manually.
3. Cross-check Nikto results with Nuclei and Burp.
4. Build a remediation list for server hardening.
5. Create repeatable Nikto scan profile for web assets.
