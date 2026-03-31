# Bash Scripting

## Why Bash Scripting Matters in Cybersecurity

Bash scripting turns repetitive command-line tasks into repeatable workflows. In security work, that means:

- Faster recon and triage
- Fewer manual mistakes
- Better reproducibility for reports and incident response
- Easy chaining of Linux tools (`grep`, `awk`, `sed`, `find`, `curl`, `nmap`, etc.)

---

## Script Basics

### Shebang

```bash
#!/usr/bin/env bash
```

- Tells the OS which interpreter to use
- `env bash` is portable across many systems

### Make executable

```bash
chmod +x script.sh
./script.sh
```

### Bash strict mode (recommended)

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'
```

- `-e`: exit on command failure
- `-u`: treat unset variables as error
- `pipefail`: fail pipeline if any command fails
- safer parsing with `IFS`

---

## Variables and Types

```bash
name="sam"
count=5
readonly api_url="https://target.local"
```

- No spaces around `=`
- Variables are strings by default
- Quote expansions unless you explicitly want word splitting

```bash
echo "$name"
```

### Command substitution

```bash
now="$(date +%F)"
kernel="$(uname -r)"
```

### Arithmetic

```bash
total=$((count + 10))
((count++))
```

---

## Input and Arguments

### Positional parameters

```bash
#!/usr/bin/env bash
echo "arg1: $1"
echo "arg2: $2"
echo "all args: $*"
echo "safe args: $@"
echo "arg count: $#"
```

Use `"$@"` in loops:

```bash
for item in "$@"; do
	echo "Processing: $item"
done
```

### Read user input

```bash
read -rp "Target IP: " target
echo "You entered: $target"
```

---

## Conditionals

### `if` statement

```bash
if [[ -f /etc/passwd ]]; then
	echo "File exists"
elif [[ -d /etc ]]; then
	echo "Directory exists"
else
	echo "Not found"
fi
```

### Useful tests

- `-f` file exists
- `-d` directory exists
- `-x` executable
- `-r` readable
- `-w` writable
- `-z` string is empty
- `-n` string is non-empty

String and numeric examples:

```bash
[[ "$user" == "root" ]]
[[ "$port" -gt 1024 ]]
```

---

## Loops

### `for`

```bash
for port in 22 80 443; do
	echo "Checking $port"
done
```

### `while`

```bash
counter=1
while [[ $counter -le 5 ]]; do
	echo "Attempt $counter"
	((counter++))
done
```

### Read file line by line safely

```bash
while IFS= read -r host; do
	echo "Scanning $host"
done < hosts.txt
```

---

## Functions

```bash
log_info() {
	local msg="$1"
	echo "[+] $msg"
}

check_root() {
	if [[ $EUID -ne 0 ]]; then
		echo "Run as root"
		return 1
	fi
}

log_info "Script started"
check_root || exit 1
```

- `local` avoids polluting global scope
- use return codes for function success/failure

---

## Exit Codes and Error Handling

- `0` means success
- non-zero means failure

```bash
command_that_might_fail || {
	echo "Command failed" >&2
	exit 1
}
```

Use `trap` for cleanup:

```bash
cleanup() {
	rm -f /tmp/tmp_scan_file
}

trap cleanup EXIT
```

---

## Parsing Options with `getopts`

```bash
#!/usr/bin/env bash
set -euo pipefail

usage() {
	echo "Usage: $0 -t target -p port"
}

target=""
port=""

while getopts ":t:p:h" opt; do
	case "$opt" in
		t) target="$OPTARG" ;;
		p) port="$OPTARG" ;;
		h) usage; exit 0 ;;
		:) echo "Option -$OPTARG requires an argument"; exit 1 ;;
		\?) echo "Invalid option: -$OPTARG"; exit 1 ;;
	esac
done

[[ -z "$target" || -z "$port" ]] && { usage; exit 1; }
echo "Target=$target Port=$port"
```

---

## Text Processing for Security Work

### `grep`

```bash
grep -Ei "error|fail|denied" auth.log
```

### `awk`

```bash
awk '{print $1, $4, $5}' access.log
```

### `sed`

```bash
sed 's/192.168.1.10/REDACTED/g' report.txt
```

### Pipelines

```bash
cat access.log | grep "POST" | awk '{print $1}' | sort | uniq -c | sort -nr
```

---

## Practical Security Scripts

### 1) Host availability checker

```bash
#!/usr/bin/env bash
set -euo pipefail

while IFS= read -r host; do
	if ping -c 1 -W 1 "$host" >/dev/null 2>&1; then
		echo "[UP]   $host"
	else
		echo "[DOWN] $host"
	fi
done < hosts.txt
```

### 2) Fast open-port check with `nc`

```bash
#!/usr/bin/env bash
set -euo pipefail

target="$1"
for port in 22 80 443 3306 8080; do
	if nc -z -w 1 "$target" "$port" 2>/dev/null; then
		echo "[OPEN] $port"
	fi
done
```

### 3) Simple log anomaly extractor

```bash
#!/usr/bin/env bash
set -euo pipefail

logfile="${1:-/var/log/auth.log}"
grep -Ei "failed password|invalid user|authentication failure" "$logfile" \
	| awk '{print $1, $2, $3, $9, $11}'
```

---

## Defensive Bash Scripting Practices

- Quote variable expansions: `"$var"`
- Avoid `eval` unless absolutely necessary
- Validate user input (regex, allowlists)
- Use absolute paths for critical commands in automation
- Limit privileges; avoid running scripts as root by default
- Use `shellcheck` to catch common bugs

Run static checks:

```bash
shellcheck script.sh
```

---

## Cron and Scheduled Scripts

### Edit crontab

```bash
crontab -e
```

Example (run every day at 02:30):

```cron
30 2 * * * /home/sam/scripts/log_review.sh >> /home/sam/log_review.out 2>&1
```

Security notes:

- Use full paths in cron jobs
- Restrict script write permissions
- Log outputs for troubleshooting and audits

---

## Debugging Bash Scripts

Enable trace mode:

```bash
bash -x script.sh
```

Inside script:

```bash
set -x   # start trace
set +x   # stop trace
```

---

## Quick Bash Cheat Sheet

- `$(cmd)` command substitution
- `$((expr))` arithmetic
- `[[ ... ]]` modern test syntax
- `"$@"` safe argument expansion
- `2>/dev/null` suppress stderr
- `>> file` append output
- `|` pipeline
- `&&` run next command only on success
- `||` run next command on failure

---

## Practice Tasks

1. Write a script to enumerate open ports from a list and store results in CSV.
2. Build a log parser that alerts when failed SSH attempts exceed a threshold.
3. Create a backup automation script with timestamped archives.
4. Parse `nmap -oG` output and extract only live hosts.
5. Build a `getopts`-based wrapper to run standardized recon checks.

Mastering Bash scripting will make your Linux and cybersecurity workflow significantly faster, more reliable, and easier to scale.
