# AWS Security

## Overview

AWS security focuses on identity-first access control, network boundary design, encryption, and deep visibility through CloudTrail/CloudWatch and security services.

---

## Account and Organization Security

Best practices:

- Use AWS Organizations with separate accounts per environment
- Restrict root user usage and enable MFA
- Use SCPs (Service Control Policies) to enforce guardrails
- Centralize security logging in a dedicated account

Useful commands:

```bash
aws sts get-caller-identity
aws organizations list-accounts
aws organizations list-policies --filter SERVICE_CONTROL_POLICY
```

---

## IAM Hardening

- Prefer IAM roles over long-term access keys
- Enforce MFA for console and sensitive API actions
- Remove wildcard actions/resources where not required
- Use permission boundaries and condition keys

Audit examples:

```bash
aws iam list-users
aws iam list-access-keys --user-name <user>
aws iam get-account-summary
aws iam generate-credential-report
aws iam get-credential-report
```

---

## Network Security in AWS

Core components:

- VPC, subnets (public/private)
- Security Groups (stateful)
- Network ACLs (stateless)
- VPC endpoints to reduce internet exposure
- AWS WAF and Shield for web/DDOS protection

Inspect security groups:

```bash
aws ec2 describe-security-groups
aws ec2 describe-security-group-rules --filters Name=group-id,Values=sg-xxxxxxxx
```

---

## S3 Security

Common risks:

- Public bucket policies
- Overly permissive ACLs
- Missing encryption and versioning

Audit and remediation examples:

```bash
aws s3api list-buckets
aws s3api get-bucket-policy --bucket <bucket>
aws s3api get-public-access-block --bucket <bucket>
aws s3api get-bucket-encryption --bucket <bucket>
aws s3api put-public-access-block --bucket <bucket> --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
```

---

## Logging and Detection

Enable and monitor:

- CloudTrail (all regions, management + data events)
- CloudWatch logs/alarms
- GuardDuty
- Security Hub
- AWS Config

Commands:

```bash
aws cloudtrail describe-trails
aws guardduty list-detectors
aws securityhub describe-hub
aws configservice describe-configuration-recorders
```

---

## Encryption and Key Management

- Use KMS CMKs for critical workloads
- Enforce encryption for EBS, S3, RDS, snapshots
- Rotate keys and monitor key usage

KMS checks:

```bash
aws kms list-keys
aws kms describe-key --key-id <key-id>
aws kms get-key-rotation-status --key-id <key-id>
```

---

## EC2 and Workload Hardening

- Use hardened AMIs
- Patch continuously (Systems Manager)
- Restrict IMDS access (prefer IMDSv2)
- Minimize instance profile permissions

IMDSv2 check:

```bash
aws ec2 describe-instances --query "Reservations[].Instances[].MetadataOptions"
```

---

## Container and Serverless Notes

- ECR image scanning enabled
- ECS/EKS task roles with least privilege
- Lambda execution role minimization
- Avoid secrets in environment variables when possible

---

## Common AWS Misconfigurations

- `0.0.0.0/0` on admin ports (22/3389)
- Public S3 buckets with sensitive data
- Unused active access keys
- No CloudTrail in all regions
- Overly broad IAM policies (`Action: *`, `Resource: *`)

---

## Incident Response Steps (AWS)

1. Identify compromised identity (`CloudTrail`, GuardDuty findings).
2. Disable/rotate credentials.
3. Quarantine affected instances/security groups.
4. Snapshot and preserve forensic evidence.
5. Eradicate persistence and validate IAM posture.

---

## Practice Tasks

1. Build an IAM least-privilege policy for S3 read-only app access.
2. Detect and remediate open security groups.
3. Enable CloudTrail + GuardDuty + Security Hub in a lab account.
4. Audit S3 buckets for public exposure and encryption gaps.
5. Enforce IMDSv2 and verify all instances comply.
