# CVEs (Common Vulnerabilities and Exposures)

## Overview

CVE is a standardized identifier for publicly known vulnerabilities (for example `CVE-2025-12345`). CVE IDs make vulnerability tracking, correlation, and communication consistent across vendors and tools.

---

## CVE Structure

Format:

- `CVE-YYYY-NNNNN`

Components:

- `YYYY`: year assigned
- `NNNNN`: sequence number

A CVE ID identifies a vulnerability but does not include full risk context by itself.

---

## CVE Ecosystem

- CNA (CVE Numbering Authority): assigns IDs
- NVD: enriches CVEs with CVSS and metadata
- Vendor advisories: patch/fix details
- Security researchers: PoCs and exploitation analysis

---

## How to Analyze a CVE

1. Read official advisory and affected versions.
2. Verify if your environment uses affected product/version.
3. Check attack vector, required privileges, and scope.
4. Review exploit maturity (PoC, weaponized, KEV listing).
5. Prioritize remediation by real exposure.

---

## Useful Sources

- NVD database
- Vendor security bulletins
- CISA KEV
- GitHub advisories and trusted research writeups

---

## CVE Triage Checklist

- Is vulnerable component present?
- Is component reachable by attacker path?
- Is exploit publicly available?
- Is auth required?
- Is there active exploitation in the wild?
- Is compensating control already in place?

---

## Example Workflow with CLI

Search local packages and versions (Linux example):

```bash
dpkg -l | grep -Ei "openssl|nginx|apache|kernel"
uname -r
```

Map version against advisory data, then test remediation in staging before production rollout.

---

## CVE Validation and False Positives

Scanners may flag vulnerable versions incorrectly when:

- backported patches exist
- component is not reachable in deployed config
- package naming/versioning differs by distro

Always validate with vendor patch notes and package changelogs.

---

## Practice Tasks

1. Pick 5 recent CVEs and perform full triage.
2. Map one CVE to affected internal assets.
3. Verify exploitability assumptions in lab.
4. Build a CVE tracking spreadsheet with owner and SLA.
5. Write remediation memo for one critical CVE.
