# Tcpdump

## Overview

Tcpdump is a command-line packet capture tool based on BPF filters. It is ideal for quick traffic captures, remote diagnostics, and incident response triage.

---

## Basic Capture

```bash
sudo tcpdump -i eth0
```

No DNS/port name resolution:

```bash
sudo tcpdump -i eth0 -nn
```

---

## Filter Examples

Host and port:

```bash
sudo tcpdump -i eth0 host 10.10.10.5 and port 443
```

TCP SYN packets:

```bash
sudo tcpdump -i eth0 'tcp[tcpflags] & tcp-syn != 0'
```

DNS traffic:

```bash
sudo tcpdump -i eth0 port 53
```

---

## Write to PCAP

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

Read capture:

```bash
tcpdump -r capture.pcap
```

---

## Incident Response Use Cases

- verify beaconing traffic
- detect unusual outbound connections
- capture exploit attempts in real time
- validate IDS/IPS alerts with raw packets

---

## Workflow

1. Define clear filter to reduce noise.
2. Capture short targeted windows.
3. Save pcap for deeper Wireshark analysis.
4. Correlate with logs and endpoint telemetry.

---

## Practice Tasks

1. Capture and isolate DNS traffic in a lab.
2. Detect SYN scan behavior from packet patterns.
3. Capture suspicious host traffic and analyze in Wireshark.
4. Create reusable tcpdump filter cheat sheet.
5. Build mini IR workflow using tcpdump + system logs.
