# Vulnerabilities Master Guide

## Overview

A vulnerability is a weakness that can be exploited to compromise confidentiality, integrity, or availability. This section focuses on how to understand, prioritize, validate, and remediate vulnerabilities in real environments.

---

## Vulnerability Lifecycle

1. Discovery (scanner, testing, threat intel, bug reports)
2. Validation (confirm exploitability and business impact)
3. Prioritization (severity + exposure + asset criticality)
4. Remediation (patch, configuration, compensating controls)
5. Verification (retest and monitor)
6. Documentation and lessons learned

---

## Key Concepts

- Vulnerability: weakness
- Threat: potential cause of unwanted impact
- Exploit: technique/code that triggers weakness
- Risk: likelihood × impact
- Exposure: accessibility of vulnerable asset

---

## Core Data Sources

- CVE records and advisories
- Vendor security bulletins
- CISA KEV catalog
- Exploit availability databases
- Internal scanner findings
- Bug bounty or pentest reports

---

## Prioritization Model (Practical)

Do not rely on CVSS alone. Combine:

- Severity score (CVSS)
- Internet exposure
- Active exploitation evidence
- Privilege required
- Asset business criticality
- Detection and containment maturity

---

## Common Pitfalls

- Treating all high CVSS equally
- Ignoring authentication/proximity constraints
- Not validating scanner false positives
- Delayed patching for internet-facing systems
- Missing owner assignment for remediation

---

## Vulnerability Management Metrics

- Mean time to remediate (MTTR)
- % critical vulns fixed in SLA window
- Reopen rate after patching
- Vulnerability recurrence by team/system
- Patch latency for externally exposed assets

---

## Reporting Template

Include for each vulnerability:

1. Title and identifier(s)
2. Affected assets and versions
3. Severity and exploitability evidence
4. Reproduction steps
5. Business impact
6. Remediation and compensating controls
7. Verification status

---

## Practice Tasks

1. Build a prioritization matrix for top 20 findings.
2. Compare CVSS-only ranking vs risk-based ranking.
3. Create remediation SLA policy by severity and exposure.
4. Track MTTR and recurrence for one month of findings.
5. Write a complete vulnerability report from lab evidence.
