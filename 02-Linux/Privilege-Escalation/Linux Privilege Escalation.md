# Linux Privilege Escalation

## Overview

Privilege escalation is the process of gaining higher privileges than initially granted. In Linux CTFs, pentests, and real incidents, it often means moving from a low-privilege user to root.

Always perform these techniques only in authorized environments.

---

## Enumeration First

Start with comprehensive local enumeration:

```bash
id
whoami
hostname
uname -a
cat /etc/os-release
sudo -l
```

Gather system and user context:

```bash
env
cat /etc/passwd
cat /etc/group
ps aux
ss -tulnp
```

---

## Key PrivEsc Vectors

### 1) Misconfigured sudo rules

Check allowed commands:

```bash
sudo -l
```

Look for:

- commands executable as root without password
- wildcards and permissive scripts
- unsafe editors/interpreters (`vim`, `less`, `python`, etc.)

Reference escalation paths from GTFOBins where applicable.

---

### 2) SUID/SGID binaries

Enumerate:

```bash
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
```

Risk: vulnerable or misconfigured SUID binaries can allow shell breakout.

---

### 3) Weak file permissions

Search critical writable locations:

```bash
find / -writable -type d 2>/dev/null | head
find /etc -writable -type f 2>/dev/null
```

Investigate writable scripts run by root (cron/systemd/startup).

---

### 4) Cron job abuse

Inspect cron configs:

```bash
cat /etc/crontab
ls -la /etc/cron.d
ls -la /etc/cron.daily
```

If root executes writable scripts/binaries, escalation may be possible.

---

### 5) PATH hijacking

If privileged scripts call commands without absolute paths, attacker-controlled binaries may execute first.

Check:

```bash
echo "$PATH"
```

---

### 6) Capabilities abuse

Linux capabilities can grant privileged actions without full root.

Enumerate:

```bash
getcap -r / 2>/dev/null
```

---

### 7) Kernel exploits

When kernel is vulnerable and local exploit exists, privilege escalation may occur.

Collect kernel version:

```bash
uname -r
```

Use trusted exploit validation processes; avoid unstable exploit execution on production systems.

---

### 8) Credentials and secrets reuse

Look for plaintext credentials:

```bash
grep -R "password\|token\|secret" /home /opt /var/www 2>/dev/null
find / -name "*.pem" -o -name "id_rsa" 2>/dev/null
```

---

## Automated Enumeration Tools

Use in lab or authorized engagements:

- `linpeas`
- `lse` (Linux Smart Enumeration)
- `linux-exploit-suggester`

Always manually verify findings.

---

## Defensive Perspective

Harden against priv esc by:

- minimizing sudo privileges
- removing unnecessary SUID bits
- patching kernel and packages regularly
- enforcing least privilege permissions
- restricting writable paths for privileged automation
- using EDR/FIM for detection

---

## Practical Enumeration Checklist

1. User and privilege context (`id`, `sudo -l`).
2. OS and kernel versions.
3. Running services and misconfigurations.
4. File permissions and writable paths.
5. Scheduled tasks and startup scripts.
6. Secrets in files, history, env vars.
7. Capabilities and special binaries.
8. Potential exploit paths with risk validation.

---

## Practice Tasks

1. Build a local enumeration script that outputs to structured sections.
2. Enumerate and classify every SUID binary on a lab machine.
3. Audit sudoers entries and explain risk per entry.
4. Simulate a writable cron script vulnerability in a VM and fix it.
5. Create a hardening report that maps each found weakness to remediation.
