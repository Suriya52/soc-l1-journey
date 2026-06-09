# 🧪 11 — Labs & Hands-on Exercises

> Theory without practice is just reading. Do the labs.

## Purpose
Practical lab work translates knowledge into demonstrable skills. Every lab here is documented with objectives, steps, findings, and lessons learned.

## Lab Index

| # | Lab Name | Platform | Topic | Report |
|---|----------|----------|-------|--------|
| L01 | SOC Analyst Intro | TryHackMe | SOC Fundamentals | [View →](./L01-SOC-Analyst-Intro/) |
| L02 | Network Fundamentals | TryHackMe | Networking | [View →](./L02-Networking/) |
| L03 | Linux PrivEsc | TryHackMe | Linux | [View →](./L03-Linux/) |
| L04 | Splunk Basics | TryHackMe | SIEM | [View →](./L04-Splunk/) |
| L05 | ELK Investigation | TryHackMe | SIEM | [View →](./L05-ELK/) |
| L06 | Phishing Analysis | BTL Online | Log Analysis | [View →](./L06-Phishing/) |
| L07 | IDS/IPS with Suricata | Home Lab | Detection | [View →](./L07-Suricata/) |

## Home Lab Setup

```
Home Lab Architecture:
┌─────────────────────────────────────────────┐
│  HOST MACHINE (Your PC/Laptop)              │
│  ┌──────────────────┐  ┌──────────────────┐ │
│  │ SIEM VM          │  │ Windows Target   │ │
│  │ ELK Stack/Wazuh  │  │ Win Server 2019  │ │
│  │ Ubuntu 22.04     │  │ AD Domain        │ │
│  └──────────────────┘  └──────────────────┘ │
│  ┌──────────────────┐  ┌──────────────────┐ │
│  │ Linux Target     │  │ Attacker VM      │ │
│  │ Ubuntu 20.04     │  │ Kali Linux       │ │
│  └──────────────────┘  └──────────────────┘ │
└─────────────────────────────────────────────┘
           VirtualBox / VMware
```

## Lab Report Template
Each lab folder must contain:
- `README.md` — objectives and summary
- `walkthrough.md` — step-by-step with screenshots
- `findings.md` — what was discovered
- `lessons-learned.md` — key takeaways
