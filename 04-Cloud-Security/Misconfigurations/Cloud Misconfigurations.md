# Cloud Misconfigurations

## Overview

Misconfigurations are one of the most common causes of cloud breaches. Most are preventable through baseline policies, automation, and continuous validation.

---

## Common High-Impact Misconfigurations

- Public storage buckets with sensitive data
- Open security groups/firewall rules on admin ports
- Excessive IAM permissions
- Missing audit logs
- Default credentials or unmanaged keys
- Kubernetes workloads running privileged
- No encryption on sensitive storage/services

---

## Why Misconfigurations Happen

- Fast cloud adoption without security guardrails
- Manual infrastructure changes outside IaC
- Drift between intended and actual state
- Poor visibility across multi-account/multi-subscription environments
- Lack of ownership for security controls

---

## Detection Methods

1. CSPM continuous scans
2. Native cloud config compliance services
3. IaC policy checks in CI/CD
4. Periodic red-team and security reviews

Example IaC checks:

```bash
checkov -d .
tfsec .
```

---

## Native Service Examples

AWS:

```bash
aws configservice describe-compliance-by-config-rule
aws securityhub get-findings --max-results 20
```

Azure:

```bash
az policy state list --top 20
az security assessment list --top 20
```

GCP:

```bash
gcloud scc findings list organizations/<org-id>/sources/- --limit=20
```

---

## Misconfiguration Management Lifecycle

1. Define baseline policy controls.
2. Detect drift and risky states continuously.
3. Prioritize by exposure and business impact.
4. Remediate with automation where possible.
5. Verify and prevent regression.

---

## Guardrail Design

- Preventive: deny policy violations before deployment
- Detective: alert on risky deployed state
- Corrective: auto-remediate approved misconfig classes

---

## Automation Ideas

- Auto-close public storage exposure
- Auto-tag and quarantine high-risk resources
- Disable stale access keys
- Block creation of internet-exposed admin ports

---

## Cloud Misconfiguration Incident Response

1. Validate exposure and potential data impact.
2. Contain quickly (policy/network/identity controls).
3. Preserve logs and evidence.
4. Rotate credentials and secrets if risk exists.
5. Implement preventive control to stop recurrence.

---

## Practice Tasks

1. Build a misconfiguration severity matrix for your cloud environment.
2. Detect all internet-exposed management ports and remediate.
3. Identify and fix top 10 IAM over-privilege findings.
4. Add CI policy checks that fail insecure IaC changes.
5. Create auto-remediation playbook for public storage findings.
