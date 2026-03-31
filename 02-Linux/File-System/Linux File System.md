# Linux File System

## File System Overview

Linux uses a hierarchical tree structure that starts at `/`.

Key principles:

- No drive letters like Windows (`C:`)
- Mount points attach disks/partitions to directories
- Most resources appear as files

---

## Filesystem Hierarchy Standard (FHS)

- `/bin`: essential user binaries
- `/sbin`: essential system binaries
- `/boot`: bootloader files and kernel
- `/dev`: device files
- `/etc`: host-specific config files
- `/home`: user home directories
- `/lib`, `/lib64`: shared libraries
- `/media`, `/mnt`: removable/media mount points
- `/opt`: optional software packages
- `/proc`: virtual process and kernel info
- `/root`: root user home
- `/run`: volatile runtime state
- `/srv`: service data
- `/sys`: kernel and hardware interfaces
- `/tmp`: temporary files
- `/usr`: userland applications and docs
- `/var`: variable data (logs, spool, cache)

---

## File Types in Linux

Use `ls -l` to identify file types:

- `-` regular file
- `d` directory
- `l` symbolic link
- `c` character device
- `b` block device
- `p` named pipe
- `s` socket

---

## Absolute vs Relative Paths

- Absolute path starts from `/`
- Relative path starts from current directory

Examples:

- Absolute: `/var/log/auth.log`
- Relative: `../logs/auth.log`

---

## Inodes and Metadata

An inode stores metadata:

- ownership
- permissions
- timestamps
- file size
- pointers to data blocks

Get inode details:

```bash
ls -li
stat file.txt
```

---

## Hard Links vs Symbolic Links

Hard link:

- points to same inode
- cannot span filesystems
- usually cannot link directories

Symbolic link:

- points to path name
- can cross filesystems
- can point to directories

```bash
ln original.txt hardlink.txt
ln -s /var/log/auth.log auth-link.log
```

---

## Mounting and Unmounting

```bash
lsblk
sudo mount /dev/sdb1 /mnt/data
mount | grep sdb1
sudo umount /mnt/data
```

Persistent mounts in `/etc/fstab`:

```fstab
UUID=xxxx-xxxx /mnt/data ext4 defaults 0 2
```

---

## Disk Usage and Capacity

```bash
df -h
du -sh /var/log/*
```

- `df`: filesystem usage
- `du`: directory/file usage

---

## File Integrity Basics

Hashing useful for forensics and verification:

```bash
sha256sum suspicious.bin
md5sum sample.bin
```

Compare known-good hash values before execution.

---

## File Search and Content Search

```bash
find / -type f -name "*.log" 2>/dev/null
find / -perm -4000 -type f 2>/dev/null
grep -R "token" /etc 2>/dev/null
```

Security use cases:

- detect SUID binaries
- identify sensitive configs
- locate unauthorized scripts

---

## File Timestamps

Linux tracks:

- atime: last access
- mtime: last content modification
- ctime: last metadata change

Check with:

```bash
stat file.txt
```

---

## Useful Archiving and Compression

```bash
tar -cvf backup.tar /etc
tar -xvf backup.tar
tar -czvf backup.tar.gz /var/log
gzip report.txt
gunzip report.txt.gz
```

---

## Special Files in /proc

- `/proc/cpuinfo`
- `/proc/meminfo`
- `/proc/<pid>/cmdline`
- `/proc/<pid>/environ`

Examples:

```bash
cat /proc/cpuinfo | head
cat /proc/meminfo | head
```

---

## Security-Focused Checks

```bash
find / -xdev -type d -perm -0002 2>/dev/null
find / -type f -name "*.pem" 2>/dev/null
find /home -type f -name ".*history" 2>/dev/null
```

These checks can reveal:

- world-writable directories
- exposed secrets
- command history leakage

---

## Practice Tasks

1. Map your system by documenting each top-level directory purpose.
2. Find top 20 largest files under `/var`.
3. Create and compare hard links and symbolic links.
4. Add and test a safe `/etc/fstab` mount entry in a lab VM.
5. Identify all SUID and SGID binaries and review necessity.
