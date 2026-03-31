# Zero-Day Vulnerabilities

## Overview

A zero-day vulnerability is a flaw unknown to the vendor or publicly disclosed without an available patch at the time of exploitation.

A zero-day exploit is active attack code using that flaw.

---

## Why Zero-Days Matter

- No immediate patch may exist
- Detection signatures can lag
- High-value targets are often prioritized by attackers
- Response relies on rapid containment and compensating controls

---

## Zero-Day Response Strategy

1. Confirm threat intelligence credibility.
2. Identify potentially affected assets fast.
3. Apply temporary mitigations/workarounds.
4. Increase monitoring for related IOC/TTP patterns.
5. Patch immediately once fix is available.

---

## Compensating Controls

- disable vulnerable feature/module
- block exploit path at WAF/firewall/IPS
- isolate exposed services
- enforce least privilege and segmentation
- add behavior-based detection rules

---

## Threat Intel Integration

Track:

- vendor advisories
- CERT/CISA alerts
- trusted researcher disclosures
- exploitation-in-the-wild indicators

Prioritize intelligence that includes clear IOC/TTP and affected versions.

---

## Detection and Hunting

- monitor for unusual process/network behavior
- hunt for exploitation artifacts in logs/EDR
- correlate suspicious events with known TTP chains
- retain forensic data for post-analysis

---

## Communication and Governance

During zero-day events:

- establish executive and technical update cadence
- maintain decision logs for mitigations
- coordinate patch windows and business impact
- document residual risk acceptance if patch delayed

---

## Post-Incident Lessons

- improve asset inventory accuracy
- reduce patch deployment time
- strengthen compensating control automation
- test emergency change workflows regularly

---

## Practice Tasks

1. Build a zero-day emergency response runbook.
2. Simulate a high-profile zero-day event tabletop exercise.
3. Map compensating controls for common service classes.
4. Create communication template for leadership updates.
5. Measure time-to-mitigation in simulation exercises.
