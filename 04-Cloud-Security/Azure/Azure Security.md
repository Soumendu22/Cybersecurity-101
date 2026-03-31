# Azure Security

## Overview

Azure security combines Microsoft Entra ID (Azure AD), role-based access control, network security controls, Defender for Cloud, and policy-driven governance.

---

## Identity and Access Security

Core controls:

- Enforce MFA and Conditional Access
- Use Privileged Identity Management (PIM)
- Minimize Global Administrator assignments
- Prefer managed identities over embedded credentials

CLI examples:

```bash
az account show
az role assignment list --all
az ad signed-in-user show
```

---

## RBAC and Least Privilege

- Assign roles at smallest possible scope
- Avoid broad `Owner` assignments
- Use custom roles for strict operations
- Periodically review role assignments

```bash
az role definition list --name Owner
az role assignment list --scope /subscriptions/<sub-id>
```

---

## Network Security

Main controls:

- Network Security Groups (NSGs)
- Azure Firewall
- Private Endpoints
- DDoS Protection
- Application Gateway WAF

Inspect NSG rules:

```bash
az network nsg list -o table
az network nsg rule list --resource-group <rg> --nsg-name <nsg>
```

---

## Storage Security

- Disable public blob access unless required
- Enforce HTTPS-only access
- Use private endpoints for sensitive storage
- Enable soft delete and versioning where applicable

```bash
az storage account list -o table
az storage account show --name <account> --resource-group <rg>
```

---

## Logging and Detection

Use:

- Azure Activity Logs
- Azure Monitor + Log Analytics
- Microsoft Defender for Cloud
- Microsoft Sentinel (SIEM)

```bash
az monitor activity-log list --max-events 20
az security pricing list
```

---

## Encryption and Key Management

- Azure Key Vault for secrets/keys/certs
- Customer-managed keys for sensitive services
- Soft-delete and purge protection enabled in Key Vault

```bash
az keyvault list -o table
az keyvault show --name <kv-name>
az keyvault secret list --vault-name <kv-name>
```

---

## VM and Compute Hardening

- Disable public IPs where unnecessary
- Use Just-In-Time VM access
- Baseline with Defender recommendations
- Patch with Azure Update Manager

```bash
az vm list -d -o table
az vm show --resource-group <rg> --name <vm>
```

---

## Governance with Azure Policy

- Enforce tagging and region restrictions
- Deny insecure SKUs/configurations
- Require encryption and private networking

```bash
az policy assignment list -o table
az policy state list --top 20
```

---

## Common Azure Misconfigurations

- Excessive Global Admins
- Publicly exposed management ports on VMs
- Storage accounts with broad network access
- Disabled diagnostic logs
- Overly permissive RBAC scope assignments

---

## Incident Response Steps (Azure)

1. Identify affected resources via Activity Log and Sentinel.
2. Contain compromised identities and sessions.
3. Isolate workloads/network paths.
4. Preserve evidence (logs, snapshots, config state).
5. Rotate secrets and enforce new controls.

---

## Practice Tasks

1. Build Conditional Access policy for admin MFA enforcement.
2. Audit and reduce high-privilege RBAC assignments.
3. Detect NSGs exposing SSH/RDP to internet.
4. Harden Key Vault with purge protection and private access.
5. Create Azure Policy assignment that denies public storage exposure.
