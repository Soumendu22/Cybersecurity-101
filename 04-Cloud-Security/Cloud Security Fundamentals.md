# Cloud Security Fundamentals

## Overview

Cloud security is about protecting identities, workloads, data, and network paths across shared-responsibility environments. Security work in cloud differs from on-prem because infrastructure is API-driven, fast-changing, and heavily identity-based.

---

## Shared Responsibility Model

Responsibilities are split between cloud provider and customer.

- Provider: physical datacenters, core platform security, hardware lifecycle
- Customer: identity design, data protection, workload hardening, configuration security

Rule: if you can configure it, you are usually responsible for securing it.

---

## Core Cloud Security Domains

1. IAM and identity hygiene
2. Network segmentation and traffic controls
3. Data encryption and key management
4. Logging, monitoring, and detection
5. Vulnerability and patch management
6. Backup, resilience, and incident response
7. Governance and continuous compliance

---

## Security Principles for Cloud

- Least privilege by default
- Deny-by-default access models
- Zero trust mindset for internal/external traffic
- Immutable and reproducible infrastructure
- Security automation first, manual exceptions second

---

## Cloud Attack Surface Examples

- Publicly exposed object storage buckets
- Over-privileged service accounts/roles
- Insecure Kubernetes control plane setup
- Misconfigured security groups/firewall rules
- Leaked access keys in repos and CI logs
- Weak metadata service protections

---

## Cloud Security Baseline Checklist

1. MFA enforced for all privileged identities.
2. No long-lived root/owner credential usage.
3. Centralized audit logging enabled and immutable.
4. Encryption at rest and in transit enforced.
5. Public exposure continuously monitored.
6. Automated misconfiguration scanning in CI/CD.
7. Incident response runbooks tested.

---

## Tooling Categories

- CSPM: cloud posture management
- SIEM/SOAR: log analysis and response automation
- CWPP: workload runtime security
- IAM analysis tools
- IaC scanners (Terraform/CloudFormation/Bicep scanners)

---

## Infrastructure as Code Security

Benefits:

- Versioned infrastructure changes
- Policy checks before deployment
- Easier rollback and auditability

Useful tools:

```bash
# Terraform formatting/validation
terraform fmt -recursive
terraform validate

# Example IaC scanning tools (install separately)
checkov -d .
tfsec .
```

---

## Secrets Management

Do not store secrets in source code or container images.

Use cloud-native secret stores and rotate credentials regularly.

Checklist:

- secret rotation policy
- access logging enabled
- minimal read scope per workload
- short-lived credentials where possible

---

## Incident Response in Cloud

1. Detect suspicious activity (alerts/log anomaly).
2. Isolate affected identity/workload/network.
3. Preserve evidence (audit logs, snapshots, metadata).
4. Contain and eradicate persistence.
5. Rotate credentials and keys.
6. Recover services and validate controls.
7. Conduct post-incident hardening review.

---

## Practice Tasks

1. Build a cloud security baseline checklist for one provider.
2. Create a least-privilege IAM policy for a sample app.
3. Enable audit logging and route logs to central storage.
4. Scan IaC templates for security issues before deployment.
5. Simulate key leakage and execute credential rotation workflow.
