# 🌐 02 — Networking Basics

> You can't defend a network you don't understand.

## Purpose
Network knowledge is the bedrock of SOC work. This section covers the protocols, models, and tools needed to read network traffic, understand communication flows, and identify anomalies.

## Topics Covered

- [ ] OSI Model (all 7 layers with security relevance)
- [ ] TCP/IP stack and the 3-way handshake
- [ ] Common protocols: HTTP/S, DNS, SMTP, FTP, SSH, RDP
- [ ] IP addressing, subnets, CIDR notation
- [ ] Ports and services (top 100 ports)
- [ ] Firewalls, proxies, and NAT
- [ ] Wireshark packet capture and analysis
- [ ] Network flow analysis (NetFlow, PCAP)
- [ ] Common network attacks (port scan, MITM, DNS poisoning)
- [ ] VPN and tunneling concepts

## Files in This Folder

| File | Description |
|------|-------------|
| `osi-model.md` | OSI layers with security context per layer |
| `tcp-ip-guide.md` | TCP/IP deep dive with packet diagrams |
| `common-protocols.md` | Protocol reference with default ports |
| `wireshark-cheatsheet.md` | Wireshark filters and analysis guide |
| `network-attacks.md` | Common network-level attack patterns |
| `ports-services-reference.md` | Top 100 ports quick reference |

## Quick Reference: Critical Ports

| Port | Protocol | Service | Security Note |
|------|----------|---------|---------------|
| 22 | TCP | SSH | Brute force target |
| 23 | TCP | Telnet | Unencrypted — flag it |
| 25 | TCP | SMTP | Phishing/spam relay |
| 53 | UDP/TCP | DNS | DNS tunneling vector |
| 80 | TCP | HTTP | Unencrypted web |
| 443 | TCP | HTTPS | Encrypted web |
| 445 | TCP | SMB | EternalBlue, ransomware |
| 3389 | TCP | RDP | Brute force / lateral movement |
| 4444 | TCP | Metasploit | Common C2 port — always alert |

## Wireshark Essential Filters

```
# Filter by IP
ip.addr == 192.168.1.100

# Show only DNS traffic
dns

# HTTP requests only
http.request

# TCP SYN packets (connection attempts)
tcp.flags.syn == 1 && tcp.flags.ack == 0

# Find large data transfers
frame.len > 1000
```
