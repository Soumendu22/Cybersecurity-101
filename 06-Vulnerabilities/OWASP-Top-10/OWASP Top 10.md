# OWASP Top 10

## Overview

OWASP Top 10 is a widely used awareness list of critical web application security risks. It is not exhaustive, but it is excellent for baseline secure development and testing programs.

---

## Current OWASP Top 10 Categories (2021)

1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery

---

## How to Use OWASP Top 10 Practically

- As secure coding training framework
- As threat modeling starter checklist
- As test planning baseline for web assessments
- As audit control map for engineering teams

---

## Mapping Examples

- IDOR -> Broken Access Control
- SQLi/XSS -> Injection
- Public debug/admin endpoints -> Security Misconfiguration
- Missing logs/alerts -> Logging and Monitoring Failures

---

## SDLC Integration

1. Design phase: threat model against Top 10 categories.
2. Build phase: secure coding checklists and code review gates.
3. Test phase: automated + manual validation per category.
4. Deploy phase: baseline hardening and logging requirements.
5. Operate phase: monitor and patch continuously.

---

## Developer-Focused Checklist

- enforce object-level access checks
- use parameterized queries
- use safe output encoding and CSP
- lock down security headers
- maintain component inventory and patch cadence
- implement strong auth/session controls

---

## Practice Tasks

1. Map one lab app weaknesses to OWASP Top 10 categories.
2. Build Top 10-based testing checklist for your team.
3. Add CI checks for common Top 10 issues.
4. Create secure code review rubric aligned to Top 10.
5. Produce quarterly trend report by OWASP category.
