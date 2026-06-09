# 🛠️ 13 — Security Tools

> Know your tools. A craftsperson is only as good as their toolbox.

## Purpose
Quick-reference cheat sheets and usage guides for common security tools used in SOC environments.

## Tools Reference

| Tool | Category | Cheat Sheet |
|------|----------|-------------|
| Wireshark | Network Analysis | [View →](./wireshark-cheatsheet.md) |
| Nmap | Network Scanner | [View →](./nmap-cheatsheet.md) |
| Splunk | SIEM | [View →](../05-SIEM/splunk/) |
| Volatility | Memory Forensics | [View →](./volatility-cheatsheet.md) |
| TheHive | SOAR/Case Mgmt | [View →](./thehive-guide.md) |
| Suricata | IDS/IPS | [View →](./suricata-guide.md) |
| MISP | Threat Intel | [View →](./misp-guide.md) |
| CyberChef | Data Analysis | [View →](./cyberchef-guide.md) |
| VirusTotal | Malware Analysis | [View →](./virustotal-guide.md) |

## Nmap Quick Reference

```bash
# Basic scan
nmap 192.168.1.0/24

# Service and version detection
nmap -sV -sC 192.168.1.100

# All ports
nmap -p- 192.168.1.100

# OS detection
nmap -O 192.168.1.100

# Stealth scan
nmap -sS 192.168.1.100

# Output to file
nmap -oA output_filename 192.168.1.100
```

## Wireshark Key Filters

```
# Follow TCP stream
Right-click packet → Follow → TCP Stream

# Export objects (files)
File → Export Objects → HTTP

# Find credentials (BE CAREFUL - lab use only)
http.authbasic
ftp.request.command == "PASS"
```
