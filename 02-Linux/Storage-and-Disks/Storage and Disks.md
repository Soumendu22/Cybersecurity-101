# Linux Storage and Disks

## Storage Concepts

Linux storage can include:

- physical disks (`/dev/sda`, `/dev/nvme0n1`)
- partitions (`/dev/sda1`)
- filesystems (`ext4`, `xfs`, `btrfs`)
- logical volumes (LVM)
- encrypted volumes (LUKS)

---

## Discover Disks and Partitions

```bash
lsblk
sudo fdisk -l
blkid
```

These commands show device layout, filesystem type, labels, and UUIDs.

---

## Partitioning Basics

`fdisk` (MBR/GPT basic) or `parted` (advanced).

Example with `fdisk`:

```bash
sudo fdisk /dev/sdb
```

Typical flow:

- create partition
- write table
- format partition
- mount and persist via `/etc/fstab`

---

## Filesystem Creation and Checking

Create ext4 filesystem:

```bash
sudo mkfs.ext4 /dev/sdb1
```

Check filesystem:

```bash
sudo fsck -f /dev/sdb1
```

---

## Mounting

Temporary mount:

```bash
sudo mount /dev/sdb1 /mnt/data
```

Persistent mount in `/etc/fstab` (recommended with UUID):

```fstab
UUID=xxxx-xxxx /mnt/data ext4 defaults,noatime 0 2
```

Validate fstab:

```bash
sudo mount -a
```

---

## Disk Usage Monitoring

```bash
df -h
du -sh /var/*
```

Find large files quickly:

```bash
find / -type f -size +500M 2>/dev/null
```

---

## LVM Overview

LVM layers:

- PV: physical volume
- VG: volume group
- LV: logical volume

Useful commands:

```bash
pvs
vgs
lvs
```

LVM enables easier resizing and storage management in servers.

---

## Swap Management

Check swap:

```bash
swapon --show
free -h
```

Create swap file (example):

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

---

## Disk Encryption (LUKS)

Basic workflow:

1. initialize encrypted container (`cryptsetup luksFormat`)
2. open mapped device (`cryptsetup open`)
3. create filesystem and mount
4. configure boot-time unlock if needed

Use only in lab first and maintain key backup strategy.

---

## Security Checks for Storage

- detect unencrypted sensitive partitions
- audit world-readable backup locations
- verify secure mount options (`nodev`, `nosuid`, `noexec`) where appropriate
- monitor free space to prevent DoS via disk exhaustion

Example mount option audit:

```bash
mount | grep -E "nosuid|noexec|nodev"
```

---

## Practice Tasks

1. Add and mount a new virtual disk in a lab VM.
2. Configure persistent mount with UUID and verify reboot behavior.
3. Create an LVM logical volume and extend it.
4. Apply secure mount options to temporary directories.
5. Build a disk usage alert script with threshold checks.
