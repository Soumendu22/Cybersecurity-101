# Linux Security Hardening

## Hardening Overview

Hardening reduces attack surface and limits impact of compromise. Effective hardening combines configuration, patching, access control, monitoring, and policy.

---

## Baseline Hardening Checklist

1. Patch OS and critical packages regularly.
2. Remove/disable unnecessary services.
3. Enforce least privilege for users and sudo.
4. Harden SSH configuration.
5. Configure host firewall.
6. Enable logging and central collection.
7. Apply file permission and integrity controls.
8. Enforce backup and recovery procedures.

---

## Account and Authentication Hardening

- disable direct root SSH login
- use key-based authentication
- enforce strong password policy
- lock inactive/stale accounts
- use MFA where possible

SSH settings in `/etc/ssh/sshd_config`:

```text
PermitRootLogin no
PasswordAuthentication no
MaxAuthTries 3
AllowUsers adminuser
```

---

## Network Hardening

- close all non-essential ports
- allowlist inbound traffic with firewall
- restrict outbound where feasible
- disable unused network services

Example UFW policy:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw enable
```

---

## Service Hardening

- run services with dedicated non-root accounts
- isolate services with systemd security directives
- disable legacy/insecure protocols
- keep web/database services minimally exposed

---

## Filesystem and Permission Hardening

- enforce strict permissions on secrets (`600`)
- remove unnecessary SUID/SGID bits
- apply `nodev`, `nosuid`, `noexec` on appropriate mounts
- restrict write access on scripts run by privileged users

---

## Kernel and Runtime Hardening

- apply kernel updates quickly for high-risk CVEs
- disable unused kernel modules
- configure sysctl for secure defaults

Sample sysctl ideas:

```text
net.ipv4.ip_forward=0
net.ipv4.conf.all.accept_source_route=0
net.ipv4.conf.all.accept_redirects=0
kernel.randomize_va_space=2
```

Apply:

```bash
sudo sysctl -p
```

---

## Mandatory Access Control

Use one of:

- AppArmor
- SELinux

Benefits:

- contains compromised services
- adds policy-based access restrictions beyond standard Unix permissions

---

## Audit and Detection Tooling

- `auditd` for syscall-level auditing
- `fail2ban` for brute-force mitigation
- file integrity tools (`AIDE`)
- endpoint detection/monitoring agents

---

## Backup and Recovery Security

- maintain offline/immutable backups
- encrypt sensitive backups
- test restoration regularly
- protect backup credentials and storage permissions

---

## Continuous Hardening Workflow

1. Assess current baseline (config + vuln scan).
2. Prioritize by risk and exposure.
3. Apply changes in staging.
4. Validate functionality and security controls.
5. Roll out and monitor.
6. Re-audit periodically.

---

## Practice Tasks

1. Harden a fresh Linux VM using this checklist and document each control.
2. Disable all unnecessary services and justify remaining ones.
3. Implement SSH key-only authentication and verify lockout controls.
4. Apply secure sysctl settings and test impact.
5. Build a monthly hardening audit report template.
