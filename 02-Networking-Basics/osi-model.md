# OSI Model — Security Context

> Every attack and defense can be mapped to an OSI layer.

## The 7 Layers

```
┌──────────────────────────────────────────────────────────┐
│  Layer 7 — APPLICATION   HTTP, DNS, SMTP, FTP            │
│  Layer 6 — PRESENTATION  Encryption, encoding, SSL/TLS   │
│  Layer 5 — SESSION       Session management, auth        │
│  Layer 4 — TRANSPORT     TCP, UDP — ports, reliability   │
│  Layer 3 — NETWORK       IP routing, ICMP                │
│  Layer 2 — DATA LINK     MAC addresses, switches, ARP    │
│  Layer 1 — PHYSICAL      Cables, wireless, hardware      │
└──────────────────────────────────────────────────────────┘
Memory Aid: "All People Seem To Need Data Processing"
```

## Layer-by-Layer Security Threats & Defenses

| Layer | Common Attacks | Defenses |
|-------|---------------|----------|
| 7 — Application | SQLi, XSS, CSRF, phishing | WAF, input validation, patching |
| 6 — Presentation | SSL stripping, weak cipher | TLS 1.3, strong cipher suites |
| 5 — Session | Session hijacking, replay | Secure session tokens, MFA |
| 4 — Transport | Port scanning, TCP SYN flood | Firewall, rate limiting |
| 3 — Network | IP spoofing, ICMP attacks | ACLs, ingress/egress filtering |
| 2 — Data Link | ARP poisoning, MAC flooding | 802.1X, DHCP snooping |
| 1 — Physical | Cable tapping, hardware theft | Physical security, locked racks |

## Where SOC Analysts Work Most

- **Layer 7** — Web app attacks, phishing, malware C2 over HTTP/DNS
- **Layer 4** — Port scans, brute force, suspicious connections
- **Layer 3** — IP-based IOCs, routing anomalies
