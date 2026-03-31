# Linux Permissions

## Why Permissions Matter

Permissions control who can read, write, or execute files and directories. In security, weak permissions are a common misconfiguration leading to data leaks or privilege escalation.

---

## Ownership Model

Each file has:

- user owner
- group owner
- permission bits

View with:

```bash
ls -l
```

Example:

```text
-rwxr-x--- 1 sam security 2048 Mar 31 10:00 script.sh
```

---

## Permission Bits

Three classes:

- user (`u`)
- group (`g`)
- others (`o`)

Three rights:

- `r` read
- `w` write
- `x` execute

For files:

- `r`: read contents
- `w`: modify contents
- `x`: execute as program/script

For directories:

- `r`: list entries
- `w`: create/delete/rename entries
- `x`: traverse directory

---

## Numeric (Octal) Permissions

- `r = 4`, `w = 2`, `x = 1`

Common modes:

- `644`: owner read/write, others read
- `755`: owner full, others read/execute
- `600`: private file
- `700`: private directory/script

Set with:

```bash
chmod 640 secrets.txt
chmod 755 script.sh
```

---

## Symbolic chmod

```bash
chmod u+x tool.sh
chmod g-w shared.txt
chmod o-rwx private.key
chmod -R u=rwX,g=rX,o= docs/
```

---

## Change Ownership

```bash
chown sam:soc analysts.txt
chown -R www-data:www-data /var/www/html
chgrp security audit.log
```

---

## Special Permission Bits

### SUID (Set User ID)

- File executes as file owner
- If owner is root, executable runs with root effective privileges

```bash
chmod u+s /path/program
find / -perm -4000 -type f 2>/dev/null
```

### SGID (Set Group ID)

- File executes with group privileges
- On directories, new files inherit directory group

```bash
chmod g+s /shared/teamdir
find / -perm -2000 -type f 2>/dev/null
```

### Sticky Bit

- On directories, only file owner/root can delete files
- Common on `/tmp`

```bash
chmod +t /shared/public
ls -ld /tmp
```

---

## Default Permissions and umask

`umask` removes bits from default creation modes.

Typical defaults:

- file base mode: `666`
- directory base mode: `777`

Example:

- umask `022` => files `644`, dirs `755`

Commands:

```bash
umask
umask 027
```

---

## Access Control Lists (ACLs)

ACLs provide finer-grained permissions beyond owner/group/others.

```bash
getfacl file.txt
setfacl -m u:alice:r file.txt
setfacl -m g:blue:w report.txt
setfacl -x u:alice file.txt
```

---

## Permission Security Checks

World-writable files:

```bash
find / -xdev -type f -perm -0002 2>/dev/null
```

World-writable directories without sticky bit:

```bash
find / -xdev -type d -perm -0002 ! -perm -1000 2>/dev/null
```

SUID/SGID enumeration:

```bash
find / -type f \( -perm -4000 -o -perm -2000 \) 2>/dev/null
```

---

## Good Security Practices

- Use least privilege
- Restrict secrets to `600`
- Avoid unnecessary SUID binaries
- Monitor permission drift in critical directories
- Use group-based access instead of broad world access

---

## Practice Tasks

1. Create a secure private notes directory for one user only.
2. Configure a shared team directory with SGID and no world access.
3. Enumerate and review all SUID binaries on a test VM.
4. Use ACLs to grant one user read-only access to a report.
5. Audit `/etc`, `/var`, and home directories for weak permissions.
