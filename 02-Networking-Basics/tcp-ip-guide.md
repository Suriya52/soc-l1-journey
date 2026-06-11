# TCP/IP Guide for SOC Analysts

## TCP 3-Way Handshake

```
Client                    Server
  │                          │
  │──── SYN ────────────────►│  "I want to connect"
  │                          │
  │◄─── SYN-ACK ────────────│  "OK, I acknowledge"
  │                          │
  │──── ACK ────────────────►│  "Connection established"
  │                          │
  │══════ DATA EXCHANGE ══════│
  │                          │
  │──── FIN ────────────────►│  "Done, closing"
```

## TCP Flags — What They Mean

| Flag | Meaning | Security Relevance |
|------|---------|-------------------|
| SYN | Start connection | Port scan = many SYN packets |
| ACK | Acknowledge | SYN flood: SYN without ACK |
| FIN | End connection | Normal teardown |
| RST | Reset / reject | Firewall blocking, closed port |
| PSH | Push data now | Data transfer |
| URG | Urgent data | Rarely used, sometimes evasion |

## Port States (Nmap)

| State | Meaning |
|-------|---------|
| Open | Service actively accepting connections |
| Closed | No service, but host is up |
| Filtered | Firewall blocking — no response |
| Open\|Filtered | Can't determine |

## Common Attack Patterns in TCP/IP

```
Port Scan     → Many SYN packets to different ports, few ACKs
SYN Flood     → Thousands of SYN packets, no ACK (DDoS)
TCP Hijacking → Attacker injects packets into established session
Idle Scan     → Stealth scan using zombie host
```
