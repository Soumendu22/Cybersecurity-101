# Nuclei

## Overview

Nuclei is a fast template-based vulnerability scanner for web, network, and cloud-related checks.

---

## Basic Usage

```bash
nuclei -u http://target.local
nuclei -l targets.txt
```

Use specific severity:

```bash
nuclei -l targets.txt -severity critical,high,medium
```

---

## Templates

Update templates:

```bash
nuclei -update-templates
```

Run specific template groups:

```bash
nuclei -l targets.txt -t cves/
nuclei -l targets.txt -t exposures/
```

---

## Output Options

```bash
nuclei -l targets.txt -json -o nuclei.json
nuclei -l targets.txt -markdown-export nuclei-report
```

---

## Workflow Guidance

1. Validate live assets first.
2. Run broad severity scan.
3. Re-run with focused templates for discovered tech stack.
4. Manually verify high-impact findings.
5. Prioritize confirmed exploitable issues.

---

## False Positive Handling

- Review response evidence for each finding
- Confirm endpoint is in intended scope
- Retest manually with Burp/curl
- Record confidence level in report

---

## Practice Tasks

1. Scan a lab target list and classify findings by severity.
2. Run CVE-only templates and validate manually.
3. Build suppression list for repeated false positives.
4. Correlate nuclei findings with nmap service data.
5. Create remediation tracker from confirmed findings.
