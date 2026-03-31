# GCP Security

## Overview

GCP security relies on IAM design, organization policies, network segmentation, centralized logging, and workload hardening across Compute Engine, GKE, and serverless services.

---

## Organization and Project Security

Best practices:

- Use org/folder/project hierarchy for separation
- Centralize logging and security operations project
- Apply organization policies for baseline controls

Commands:

```bash
gcloud organizations list
gcloud projects list
gcloud resource-manager folders list --organization=<org-id>
```

---

## IAM Hardening in GCP

- Grant predefined/custom roles minimally
- Avoid primitive roles (`Owner`, `Editor`) where possible
- Use service accounts with narrow scopes
- Rotate and eliminate service account keys

Audit examples:

```bash
gcloud projects get-iam-policy <project-id>
gcloud iam service-accounts list --project <project-id>
gcloud iam service-accounts keys list --iam-account <sa-email>
```

---

## Network Security

- Restrict VPC firewall rules
- Use private Google access and private clusters where possible
- Control egress using Cloud NAT and policies

```bash
gcloud compute firewall-rules list
gcloud compute networks list
gcloud compute networks subnets list --regions=all
```

---

## Storage and Data Security

- Harden Cloud Storage bucket access
- Enforce uniform bucket-level access
- Use CMEK for sensitive data sets

```bash
gcloud storage buckets list
gcloud storage buckets describe gs://<bucket>
```

---

## Logging, Detection, and Visibility

Use:

- Cloud Audit Logs
- Security Command Center
- Cloud Logging and alert policies

```bash
gcloud logging sinks list
gcloud logging metrics list
gcloud scc findings list organizations/<org-id>/sources/- --limit=20
```

---

## Compute and Metadata Security

- Minimize public IP use
- Shielded VM where possible
- Restrict metadata exposure and use workload identity patterns

```bash
gcloud compute instances list
gcloud compute instances describe <instance> --zone <zone>
```

---

## GKE Security Highlights

- Private cluster and authorized networks for control plane
- RBAC and workload identity
- Admission controls and policy enforcement
- Image scanning and signed artifacts

```bash
gcloud container clusters list
gcloud container clusters describe <cluster> --zone <zone>
```

---

## Common GCP Misconfigurations

- Overuse of `Editor` role
- Publicly exposed firewall rules
- Service account keys unmanaged
- Disabled audit logs
- Buckets with over-broad permissions

---

## Incident Response Steps (GCP)

1. Identify suspicious principals and API calls in Audit Logs.
2. Disable compromised accounts/keys.
3. Isolate affected instances/workloads.
4. Snapshot and preserve evidence.
5. Remediate IAM/network policy gaps and monitor.

---

## Practice Tasks

1. Remove primitive roles and replace with scoped roles.
2. Audit service account keys and rotate/remove old keys.
3. Detect firewall rules exposing management ports.
4. Enable SCC and review top high-risk findings.
5. Harden GKE cluster access and workload identity settings.
