# Cloud IAM Security

## Overview

Identity and Access Management (IAM) is the control plane of cloud security. Most cloud breaches involve identity abuse, token theft, privilege escalation, or permission misconfiguration.

---

## IAM Core Concepts

- Principals: users, groups, roles, service accounts, managed identities
- Permissions: allowed actions on resources
- Policies: rule sets defining access
- Trust relationships: who can assume/impersonate roles
- Conditions: context constraints (time, source IP, MFA, tags)

---

## IAM Threats

- Over-privileged identities
- Long-lived static credentials
- Credential leakage in repos/logs
- Role chaining to escalate privileges
- Excessive trust policies
- Inactive but still privileged accounts

---

## Least Privilege Strategy

1. Start from deny-all default.
2. Grant minimum actions required per workload.
3. Scope resource access narrowly.
4. Add conditions (MFA, network, session restrictions).
5. Continuously review and reduce permissions.

---

## Human vs Workload Identity

Human identity:

- SSO + MFA mandatory
- short session duration
- privileged roles via just-in-time elevation

Workload identity:

- no embedded static keys
- role/service account per workload
- scope tightly to resource operations

---

## Access Review Checklist

- Any wildcard policies (`*`) still active?
- Any dormant users with high privilege?
- Any service accounts with broad admin rights?
- Any root/owner-style account used recently?
- Any stale keys older than policy threshold?

---

## Multi-Cloud IAM Command Examples

AWS:

```bash
aws iam list-users
aws iam list-roles
aws iam get-account-authorization-details
```

Azure:

```bash
az role assignment list --all
az ad user list --top 20
```

GCP:

```bash
gcloud projects get-iam-policy <project-id>
gcloud iam service-accounts list --project <project-id>
```

---

## Privileged Access Management

- Require approval workflows for high-impact roles
- Time-bound privileged assignments
- Session recording where possible
- Emergency break-glass accounts monitored strictly

---

## IAM Logging and Detection

Monitor for:

- new admin role assignments
- policy changes adding broad access
- new access key creation
- unusual role assumptions from unexpected geos/IPs

---

## Incident Response for IAM Compromise

1. Disable compromised identity and revoke sessions.
2. Rotate keys/secrets/tokens.
3. Review audit trails for lateral movement.
4. Remove unauthorized policy changes.
5. Enforce additional controls (MFA/conditional rules).

---

## Practice Tasks

1. Build least-privilege policy for a web app + storage access.
2. Identify and remove wildcard permissions in a lab tenant.
3. Audit service accounts/roles and justify each privilege.
4. Simulate key exposure and run credential rotation workflow.
5. Create alerts for privilege escalation IAM events.
