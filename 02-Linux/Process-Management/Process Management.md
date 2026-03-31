# Linux Process Management

## What Is a Process

A process is a running instance of a program with:

- PID (process ID)
- memory space
- open files and sockets
- execution state

Each process has a parent process (PPID), except PID 1 (`systemd` on most modern systems).

---

## Process States (Common)

- `R`: Running
- `S`: Sleeping (interruptible)
- `D`: Uninterruptible sleep (often I/O)
- `T`: Stopped/traced
- `Z`: Zombie (terminated but not reaped)

---

## View Processes

```bash
ps aux
ps -ef
pstree -p
top
htop
```

Useful `ps` output columns:

- `USER`, `PID`, `%CPU`, `%MEM`, `STAT`, `COMMAND`

---

## Find Specific Processes

```bash
pgrep sshd
pgrep -af python
pidof nginx
```

Use with `xargs` safely:

```bash
pgrep -f "my_script.sh" | xargs -r kill
```

---

## Signals and Termination

```bash
kill -15 <pid>
kill -9 <pid>
pkill -f "pattern"
killall firefox
```

Common signals:

- `SIGTERM` (15): graceful shutdown
- `SIGKILL` (9): force kill
- `SIGHUP` (1): reload/terminal hangup behavior
- `SIGINT` (2): interrupt (`Ctrl + C`)

---

## Foreground and Background Jobs

```bash
sleep 100 &
jobs
fg %1
bg %1
disown -h %1
```

Shortcuts:

- `Ctrl + Z`: suspend process
- `bg`: resume in background

---

## Process Priority and Scheduling

Niceness controls scheduling preference:

```bash
nice -n 10 long_task.sh
renice -n 5 -p <pid>
```

- Lower nice value => higher priority (root required for negative values)

---

## Monitoring Resource Usage

CPU and memory:

```bash
top
free -h
vmstat 1 5
```

Per process memory map:

```bash
pmap <pid>
```

Open files and sockets:

```bash
lsof -p <pid>
lsof -i
```

---

## Startup and Service Processes

On systemd systems:

```bash
systemctl list-units --type=service
systemctl status ssh
```

Identify long-running daemons for attack surface analysis.

---

## Process Troubleshooting Workflow

1. Detect issue (`top`, alerts, logs).
2. Identify process (`ps`, `pgrep`, `systemctl status`).
3. Check files/sockets (`lsof`, `ss -tulnp`).
4. Inspect logs (`journalctl`, app logs).
5. Apply controlled action (`SIGTERM`, restart service).
6. Validate recovery and monitor.

---

## Security Use Cases

- Detect suspicious long-running reverse shells
- Identify crypto-miners through high CPU usage
- Trace unknown listeners to process IDs
- Spot orphaned/zombie process anomalies
- Review unexpected child processes under privileged daemons

---

## One-Liners for Security

```bash
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
ss -tulnp
lsof -iTCP -sTCP:LISTEN -Pn
```

Correlate listener PIDs with binaries:

```bash
readlink -f /proc/<pid>/exe
```

---

## Practice Tasks

1. Start multiple background jobs and manage them with `jobs`, `fg`, and `bg`.
2. Simulate a high CPU process and re-prioritize it with `renice`.
3. Map all listening services to their executables.
4. Create a script that alerts when a process exceeds a CPU threshold.
5. Analyze and explain parent-child process trees for web server workers.
