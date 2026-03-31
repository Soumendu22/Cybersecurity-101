# Linux Package Management

## Why Package Management Matters

Package managers install, update, verify, and remove software with dependency handling. In security operations, proper package hygiene reduces vulnerabilities and improves system stability.

---

## Debian/Ubuntu: APT and DPKG

Update package metadata:

```bash
sudo apt update
```

Upgrade packages:

```bash
sudo apt upgrade
sudo apt full-upgrade
```

Install/remove packages:

```bash
sudo apt install nmap
sudo apt remove nmap
sudo apt purge nmap
```

Search and inspect:

```bash
apt search wireshark
apt show openssh-server
dpkg -l | grep openssh
```

Fix broken dependencies:

```bash
sudo apt --fix-broken install
```

---

## RHEL/Fedora: DNF/YUM and RPM

```bash
sudo dnf check-update
sudo dnf upgrade
sudo dnf install nmap
sudo dnf remove nmap
rpm -qa | grep openssh
rpm -qi openssh-server
```

---

## Arch Linux: pacman

```bash
sudo pacman -Syu
sudo pacman -S nmap
sudo pacman -R nmap
pacman -Qs wireshark
```

---

## Repository Management

Security guidelines:

- use trusted official repos
- verify GPG signatures
- avoid random third-party repositories
- pin package versions in controlled environments

APT repo files:

- `/etc/apt/sources.list`
- `/etc/apt/sources.list.d/`

---

## Package Verification and Integrity

APT signature checks are automatic when configured correctly.

RPM signature validation:

```bash
rpm -K package.rpm
```

Manual file hash check:

```bash
sha256sum package_file
```

---

## Security Updates and Patch Strategy

Prioritize updates for:

- internet-facing services
- authentication and crypto libraries
- kernel vulnerabilities with known exploitation

Basic patch workflow:

1. inventory installed packages
2. check advisories/CVEs
3. patch in staging
4. test critical services
5. rollout and monitor

---

## Auto-Update Considerations

Useful for reducing patch lag but requires control.

- Ubuntu: `unattended-upgrades`
- RHEL/Fedora: `dnf-automatic`

Balance security and availability with maintenance windows.

---

## Useful Commands for Auditing

```bash
dpkg -l
apt list --upgradable
dnf list updates
rpm -Va
```

- `rpm -Va` can highlight modified files (needs careful interpretation)

---

## Practice Tasks

1. Build a patching checklist for a Linux web server.
2. Audit all upgradable packages and map to CVE severity.
3. Configure automatic security updates in a lab VM.
4. Validate package signatures before manual installation.
5. Document rollback strategy for failed package updates.
