# Linux Logs and Monitoring

## Why Logging Matters

Logs are critical for detection, forensics, troubleshooting, and compliance. In Linux environments, logs can reveal:

- brute-force attempts
- service failures
- privilege abuse
- suspicious process/network activity

---

## Main Log Locations

Common files in `/var/log`:

- `/var/log/auth.log` or `/var/log/secure`
- `/var/log/syslog` or `/var/log/messages`
- `/var/log/kern.log`
- web logs: `/var/log/nginx/`, `/var/log/apache2/`

Systemd journal:

- accessed via `journalctl`

---

## Basic Log Review Commands

```bash
less /var/log/auth.log
tail -f /var/log/auth.log
grep -Ei "failed|error|denied" /var/log/syslog
```

Frequency analysis:

```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

---

## journalctl Essentials

```bash
journalctl -xe
journalctl -u ssh
journalctl --since "1 hour ago"
journalctl -p err..alert
```

Persistent journald storage may need explicit config in `/etc/systemd/journald.conf`.

---

## Log Rotation

Managed by `logrotate`.

Inspect config:

```bash
cat /etc/logrotate.conf
ls /etc/logrotate.d
```

Why important:

- prevent disk exhaustion
- keep manageable retention
- compress/archive old logs

---

## Monitoring Key Signals

- repeated authentication failures
- sudden privilege escalations
- unexpected service restarts
- new listening ports
- abnormal process execution patterns

---

## Useful Monitoring Commands

```bash
watch -n 2 "ss -tulnp"
watch -n 2 "ps aux --sort=-%cpu | head"
```

File change monitoring options:

- `auditd`
- `inotify`-based tools
- endpoint detection tools

---

## Detection Examples

Failed SSH attempts:

```bash
grep "Failed password" /var/log/auth.log | wc -l
```

Successful sudo executions:

```bash
grep "sudo:" /var/log/auth.log
```

New users created:

```bash
grep -Ei "useradd|new user" /var/log/auth.log /var/log/secure 2>/dev/null
```

---

## Centralized Logging

For production, centralize logs using:

- syslog forwarders
- SIEM platforms
- agent-based log shippers

Benefits:

- tamper resistance
- correlation across hosts
- long-term retention and alerting

---

## Practice Tasks

1. Build a Bash script that summarizes failed auth attempts per IP.
2. Configure and test custom logrotate policy for app logs.
3. Correlate SSH login events with sudo activity over a time window.
4. Alert when new listening ports appear.
5. Forward logs from a Linux VM to a central syslog collector.
