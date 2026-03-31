# Wireshark

## Overview

Wireshark is a packet analysis tool used for network troubleshooting, protocol understanding, incident response, and threat investigation.

---

## Capture Basics

1. Choose interface (eth0, wlan0, tun0, etc.).
2. Start capture.
3. Apply display filters.
4. Follow streams and extract indicators.

---

## Capture Filters vs Display Filters

Capture filters (BPF) reduce captured traffic:

```text
host 10.10.10.5 and port 443
```

Display filters refine view after capture:

```text
ip.addr == 10.10.10.5 && tcp.port == 443
```

---

## Useful Display Filters

- `http`
- `dns`
- `tls`
- `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- `ip.addr == 10.10.10.10`
- `frame contains "password"`

---

## Practical Analysis Tasks

- Identify top talkers and unusual endpoints
- Detect failed connections and retransmissions
- Inspect DNS queries for suspicious domains
- Review HTTP requests for credential leakage
- Analyze TLS handshake metadata

---

## Follow Streams

Right-click packet -> Follow -> TCP/HTTP stream.

Use this to:

- reconstruct application conversations
- detect sensitive data exposure
- verify exploit traffic patterns

---

## Exporting Artifacts

- Export selected packets
- Export objects (HTTP files)
- Save filtered captures for reports

---

## Performance Tips

- Use capture filters for high-throughput links
- Stop long captures and segment by timeframe
- Disable name resolution when speed matters

---

## Security Investigation Examples

1. Suspicious beaconing pattern every fixed interval.
2. DNS tunneling indicators (long/random subdomains).
3. Lateral movement using SMB or RDP traffic spikes.
4. Credential leaks via plaintext protocols.

---

## Practice Tasks

1. Capture and filter DNS + HTTP traffic from a lab machine.
2. Identify all unique external destinations.
3. Reconstruct one HTTP transaction end-to-end.
4. Detect scanning behavior using TCP SYN patterns.
5. Build a short incident timeline from packet evidence.
