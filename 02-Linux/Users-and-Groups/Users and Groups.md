# Linux Users and Groups

## Account Model

Linux is multi-user by design. Every process runs in a user and group context.

Core identifiers:

- UID: user ID
- GID: group ID
- supplementary groups

Check identity:

```bash
id
whoami
groups
```

---

## Account Databases

- `/etc/passwd`: user account metadata
- `/etc/shadow`: password hashes and aging data
- `/etc/group`: group definitions
- `/etc/gshadow`: secure group data

Inspect safely:

```bash
cat /etc/passwd
sudo cat /etc/shadow
cat /etc/group
```

---

## User Management Commands

Create user:

```bash
sudo useradd -m -s /bin/bash analyst
sudo passwd analyst
```

Delete user:

```bash
sudo userdel -r analyst
```

Modify user:

```bash
sudo usermod -aG sudo analyst
sudo usermod -s /usr/sbin/nologin serviceuser
```

---

## Group Management

```bash
sudo groupadd security
sudo usermod -aG security analyst
sudo gpasswd -d analyst security
```

Use groups to assign shared access instead of broad permissions.

---

## Sudo and Privilege Delegation

View sudo access:

```bash
sudo -l
```

Edit policy safely:

```bash
sudo visudo
```

Best practices:

- grant least privilege commands
- avoid `ALL=(ALL) NOPASSWD: ALL` unless absolutely required
- audit sudo usage logs regularly

---

## Account Security Controls

Password aging:

```bash
chage -l analyst
sudo chage -M 90 -m 7 -W 14 analyst
```

Lock/unlock accounts:

```bash
sudo usermod -L analyst
sudo usermod -U analyst
```

Disable shell for service accounts:

```bash
sudo usermod -s /usr/sbin/nologin svcaccount
```

---

## Login and Session Monitoring

```bash
who
w
last
lastlog
```

Security value:

- identify unusual login times/locations
- detect dormant but active accounts

---

## SSH User Access Controls

In `/etc/ssh/sshd_config`:

- `PermitRootLogin no`
- `PasswordAuthentication no` (prefer keys)
- `AllowUsers` / `AllowGroups`

Restart service after changes:

```bash
sudo systemctl restart ssh
```

---

## Security Auditing Checks

- users with UID 0 besides root
- users with interactive shells unexpectedly
- stale accounts not used in long periods
- broad sudo privileges

Examples:

```bash
awk -F: '($3 == 0) {print $1}' /etc/passwd
awk -F: '($7 ~ /(bash|sh|zsh)$/) {print $1}' /etc/passwd
```

---

## Practice Tasks

1. Create role-based groups for Dev, Ops, and Security.
2. Restrict sudo privileges to specific administrative commands.
3. Audit all local accounts and classify service vs human users.
4. Enforce password aging and lock inactive accounts.
5. Harden SSH to allow only key-based login for selected users.
