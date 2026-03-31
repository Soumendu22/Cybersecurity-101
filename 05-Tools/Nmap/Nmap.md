# Nmap

## Overview

Nmap is a network mapper used for host discovery, port scanning, service/version detection, and script-based security checks.

---

## Basic Syntax

```bash
nmap [scan type] [options] <target>
```

Examples:

```bash
nmap 10.10.10.10
nmap -p- 10.10.10.10
nmap -sV -sC 10.10.10.10
```

---

## Common Scan Types

- `-sS`: SYN scan (stealthier, requires privileges)
- `-sT`: TCP connect scan
- `-sU`: UDP scan
- `-sn`: host discovery only (no port scan)

---

## High-Value Flags

- `-p-`: all TCP ports
- `-p 80,443,8080`: specific ports
- `-sV`: service/version detection
- `-O`: OS detection
- `-A`: aggressive scan (version, scripts, traceroute)
- `-T0..5`: timing template
- `--open`: show only open ports

---

## NSE Script Usage

Nmap Scripting Engine (NSE) helps with protocol/service checks.

```bash
nmap --script vuln 10.10.10.10
nmap --script http-enum -p80,443 10.10.10.10
nmap --script smb-os-discovery -p445 10.10.10.10
```

---

## Output Formats

```bash
nmap -oN scan.txt 10.10.10.10
nmap -oX scan.xml 10.10.10.10
nmap -oG scan.gnmap 10.10.10.10
nmap -oA fullscan 10.10.10.10
```

Use `-oA` for normalized multi-format reporting.

---

## Practical Workflow

1. Host discovery (`-sn`) in scope range.
2. Full port scan (`-p-`) on live hosts.
3. Service detection on discovered ports.
4. Targeted NSE scripts by service.
5. Validate manually with service-specific tools.

---

## Performance and Safety

- Avoid noisy `-T5` unless explicitly allowed
- Rate-limit scans in fragile environments
- Split scans per subnet/host for easier analysis

---

## Common Mistakes

- Running only default 1000 ports and missing services
- Trusting service banners without manual verification
- Using aggressive scans too early
- Not saving output consistently

---

## Practice Tasks

1. Scan a host with full TCP port coverage and service detection.
2. Compare results between `-sS` and `-sT` in a lab.
3. Run targeted NSE scripts based on discovered services.
4. Parse `gnmap` output to list live hosts and open ports.
5. Build an end-to-end recon report from nmap outputs.
