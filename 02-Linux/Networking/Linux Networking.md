# Linux Networking

## Networking Fundamentals in Linux

Linux networking is interface-based and managed through kernel networking stack tools. In security operations, Linux is used for:

- reconnaissance and scanning
- traffic inspection
- service exposure auditing
- firewall and routing control

---

## Interfaces and Addresses

View interfaces:

```bash
ip a
ip -br a
```

Bring interface up/down:

```bash
sudo ip link set eth0 down
sudo ip link set eth0 up
```

Assign temporary IP:

```bash
sudo ip addr add 192.168.1.50/24 dev eth0
```

---

## Routing

View route table:

```bash
ip route
```

Add route:

```bash
sudo ip route add 10.10.0.0/16 via 192.168.1.1
```

Delete route:

```bash
sudo ip route del 10.10.0.0/16
```

---

## DNS Configuration

Check DNS resolvers:

```bash
cat /etc/resolv.conf
```

Query DNS:

```bash
dig example.com
nslookup example.com
host example.com
```

Useful for enumeration and troubleshooting name resolution failures.

---

## Socket and Port Inspection

Modern command:

```bash
ss -tulnp
```

Legacy (if installed):

```bash
netstat -tulnp
```

Filter listening TCP:

```bash
ss -ltnp
```

---

## Connectivity Testing

```bash
ping -c 4 8.8.8.8
traceroute 8.8.8.8
mtr -rw 8.8.8.8
curl -I https://example.com
nc -vz 10.10.10.10 22
```

---

## Packet Capture Basics

```bash
sudo tcpdump -i eth0
sudo tcpdump -i eth0 port 53
sudo tcpdump -i eth0 -nn host 10.10.10.5
sudo tcpdump -i eth0 -w capture.pcap
```

Use captured PCAP in Wireshark for deeper analysis.

---

## Firewall Essentials

### nftables (modern)

```bash
sudo nft list ruleset
```

### iptables (legacy/common)

```bash
sudo iptables -L -n -v
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -j DROP
```

### UFW (Ubuntu simplified frontend)

```bash
sudo ufw status verbose
sudo ufw allow 22/tcp
sudo ufw enable
```

---

## Network Service Discovery

```bash
nmap -sV 192.168.1.10
nmap -sC -p- 192.168.1.10
```

Map discovered services back to local listeners with `ss` and `systemctl`.

---

## SSH Basics

```bash
ssh user@host
ssh -i id_rsa user@host
scp file.txt user@host:/tmp/
```

Security checks:

- disable password auth where possible
- prefer key-based auth
- review `/etc/ssh/sshd_config`

---

## Common Networking Files

- `/etc/hosts`
- `/etc/resolv.conf`
- `/etc/nsswitch.conf`
- `/etc/ssh/sshd_config`
- distro-specific network config files (`/etc/netplan`, `/etc/network/interfaces`)

---

## Incident Response Networking Checks

1. Identify suspicious listeners (`ss -tulnp`).
2. Map PIDs to executables (`readlink -f /proc/<pid>/exe`).
3. Check established outbound sessions.
4. Capture suspicious traffic (`tcpdump`).
5. Correlate with logs (`journalctl`, app logs, auth logs).

---

## Practice Tasks

1. Enumerate all listening ports and identify owning services.
2. Simulate DNS failures and troubleshoot resolver path.
3. Capture and filter only HTTP and DNS traffic with `tcpdump`.
4. Implement basic ingress firewall policy and validate access.
5. Build a script that checks critical service ports and alerts on changes.
