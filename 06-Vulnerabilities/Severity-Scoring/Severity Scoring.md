# Severity Scoring and Risk Prioritization

## Overview

Severity scoring helps compare vulnerabilities, but operational prioritization requires business context and exploit intelligence.

---

## CVSS Basics

CVSS captures technical severity using:

- Base metrics (intrinsic properties)
- Temporal metrics (exploit maturity/remediation level)
- Environmental metrics (organization-specific context)

---

## CVSS Vector Example

```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

Interpretation:

- network exploitable
- low complexity
- no privileges needed
- no user interaction
- high CIA impact

---

## Severity Bands (Common)

- 0.0: None
- 0.1 - 3.9: Low
- 4.0 - 6.9: Medium
- 7.0 - 8.9: High
- 9.0 - 10.0: Critical

---

## Beyond CVSS: Practical Risk Formula

Use additional modifiers:

- internet exposure
- exploit availability
- asset criticality
- lateral movement potential
- detection/response maturity

A medium CVSS on an exposed payment API may outrank a high CVSS on an isolated dev host.

---

## Prioritization Workflow

1. Compute/collect severity score.
2. Map affected business service and owner.
3. Add exploit and exposure context.
4. Assign remediation SLA.
5. Track to closure and retest.

---

## SLA Example Model

- Critical + internet exposed + exploitable: 24-72 hours
- Critical internal or hard-to-exploit: 7 days
- High: 14 days
- Medium: 30-60 days
- Low: risk-accepted or backlog with controls

---

## Reporting Metrics

- open findings by severity
- SLA breach counts
- average remediation time by severity
- recurring vulnerability classes

---

## Practice Tasks

1. Score 10 vulnerabilities using CVSS vectors.
2. Re-rank with exposure and exploit context.
3. Define SLA policy for your environment.
4. Build dashboard tracking SLA breaches.
5. Present risk-based patch plan to stakeholders.
