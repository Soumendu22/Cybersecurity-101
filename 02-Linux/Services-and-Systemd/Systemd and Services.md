# Systemd and Services

## What Is systemd

`systemd` is the service manager and init system on many Linux distributions. It starts services at boot, manages dependencies, and provides centralized logs with journald.

---

## Service Lifecycle Commands

```bash
sudo systemctl status ssh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl reload nginx
```

Enable/disable at boot:

```bash
sudo systemctl enable ssh
sudo systemctl disable ssh
```

---

## Listing Units

```bash
systemctl list-units --type=service
systemctl list-unit-files --type=service
systemctl --failed
```

Useful for incident response when identifying unexpected active services.

---

## Unit Files

Unit file paths:

- `/usr/lib/systemd/system/` or `/lib/systemd/system/` (package-managed)
- `/etc/systemd/system/` (local overrides/custom)

View unit definition:

```bash
systemctl cat ssh
```

---

## Create a Custom Service

Example unit:

```ini
[Unit]
Description=Custom Security Monitor
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/security-monitor.sh
Restart=on-failure
User=root

[Install]
WantedBy=multi-user.target
```

After creating a unit:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now security-monitor
```

---

## Service Security Hardening Options

In unit files, consider:

- `NoNewPrivileges=true`
- `PrivateTmp=true`
- `ProtectSystem=strict`
- `ProtectHome=true`
- `CapabilityBoundingSet=`
- `User=` non-root service account where possible

These reduce impact of service compromise.

---

## Journald Integration

View logs by service:

```bash
journalctl -u ssh
journalctl -u nginx -n 100 --no-pager
journalctl -u myservice -f
```

Time filters:

```bash
journalctl --since "2026-03-31 10:00:00"
journalctl --since yesterday
```

---

## Startup Analysis

```bash
systemd-analyze
systemd-analyze blame
systemd-analyze critical-chain
```

Useful for boot troubleshooting and understanding dependency bottlenecks.

---

## Security Auditing for Services

- identify unnecessary enabled services
- check services running as root
- inspect writable service binaries/scripts
- validate unit file integrity and source
- monitor unexpected service creation

---

## Practice Tasks

1. Write and deploy a custom systemd service in a lab.
2. Apply hardening directives and test service behavior.
3. Enumerate all enabled services and justify necessity.
4. Trace a failed service startup with `journalctl` and fix it.
5. Build a script to alert on newly added unit files.
