# Linux Basics

## What Is Linux

Linux is a Unix-like operating system kernel plus userland tools and distributions (Ubuntu, Debian, Kali, Fedora, Arch, etc.). In cybersecurity, Linux is widely used for:

- Offensive security tooling
- Defensive monitoring and hardening
- Server infrastructure and cloud workloads
- Automation and scripting

---

## Common Distributions in Security

- Kali Linux: penetration testing distribution with many preinstalled tools
- Ubuntu: stable and common for servers and labs
- Debian: conservative and stable package ecosystem
- Arch: rolling release, highly customizable
- CentOS/RHEL/AlmaLinux/Rocky: enterprise environments

---

## Core Linux Concepts

- Everything is treated like a file (devices, sockets, pipes)
- Multi-user by design
- Permissions and ownership control access
- Processes represent running programs
- Package managers install and maintain software

---

## Command-Line Navigation

```bash
pwd
ls -la
cd /etc
cd ~
cd -
```

Useful options:

- `ls -l`: long listing
- `ls -a`: include hidden files
- `ls -h`: human-readable sizes

---

## Working with Files and Directories

```bash
touch notes.txt
mkdir lab
cp source.txt backup.txt
mv old.txt new.txt
rm file.txt
rm -r folder/
```

Safety tips:

- prefer `cp -i` and `mv -i` for prompts in sensitive environments
- be careful with `rm -rf`

---

## Viewing and Editing Content

```bash
cat file.txt
less /var/log/syslog
head -n 20 file.txt
tail -f /var/log/auth.log
nano file.txt
vim file.txt
```

---

## Finding Files and Searching Text

```bash
find /etc -name "*.conf"
find / -type f -perm -4000 2>/dev/null
grep -R "password" /etc 2>/dev/null
```

---

## Input, Output, and Redirection

- `>` overwrite output file
- `>>` append output
- `2>` redirect stderr
- `|` pipe output to another command

```bash
ip a > interfaces.txt
nmap -sV 10.10.10.5 > scan.txt 2> scan.err
cat access.log | grep "POST" | wc -l
```

---

## Users and Privileges

Check identity and privilege context:

```bash
whoami
id
groups
sudo -l
```

- `root` has UID 0 and unrestricted permissions
- `sudo` allows controlled privilege elevation

---

## Package Management (Quick Intro)

Debian/Ubuntu:

```bash
sudo apt update
sudo apt install curl
sudo apt remove curl
```

RHEL-based:

```bash
sudo dnf install curl
```

---

## System Information Commands

```bash
uname -a
hostnamectl
cat /etc/os-release
lscpu
free -h
df -h
```

---

## Networking Basics Commands

```bash
ip a
ip r
ss -tulnp
ping -c 4 8.8.8.8
curl -I https://example.com
```

---

## Important Directories

- `/` root of filesystem
- `/home` user home directories
- `/etc` system configuration
- `/var/log` logs
- `/tmp` temporary files
- `/usr/bin` user commands
- `/bin` essential commands
- `/opt` optional applications

---

## Helpful Keyboard Shortcuts

- `Ctrl + C`: stop current process
- `Ctrl + Z`: suspend process
- `Ctrl + D`: end input/logout
- `Ctrl + R`: search command history
- `!!`: run previous command

---

## Linux Basics for Security Work

- Learn to inspect logs quickly (`grep`, `tail -f`)
- Understand permissions and ownership deeply
- Become confident with process and network inspection tools
- Automate repetitive tasks with Bash

---

## Practice Tasks

1. Create a new user and verify group membership.
2. Find all world-writable files under `/tmp`.
3. Redirect output of `ip a` and parse interface names.
4. Search logs for failed authentication events.
5. Build an alias file for your most-used security commands.
