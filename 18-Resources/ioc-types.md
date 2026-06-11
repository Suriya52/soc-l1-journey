# IOC Types Reference

## What is an IOC?

An **Indicator of Compromise (IOC)** is a piece of forensic data that identifies potentially malicious activity. Collecting and sharing IOCs helps defenders block known threats.

## IOC Types

| Type | Examples | Where Found | Tools |
|------|---------|-------------|-------|
| **IP Address** | 45.33.32.156 | Firewall, proxy, DNS logs | VirusTotal, AbuseIPDB |
| **Domain** | evil-c2.com | DNS logs, proxy logs | VirusTotal, URLScan |
| **URL** | http://evil.com/payload.exe | Proxy logs, email | URLScan, VirusTotal |
| **Email Address** | attacker@phish.com | Email gateway | MXToolbox |
| **File Hash (MD5)** | d41d8cd98f00b204e9800998ecf8427e | EDR, AV | VirusTotal |
| **File Hash (SHA256)** | e3b0c44298fc1c149... | EDR, AV | VirusTotal |
| **File Name** | invoice_2024.exe | File system logs | Cross-environment search |
| **Registry Key** | HKCU\...\Run\malware | Sysmon, EDR | Hunt in SIEM |
| **Mutex** | Global\{malware-guid} | Sandbox reports | Sandbox analysis |
| **User Agent** | "python-requests/2.28" | Proxy, web logs | Proxy analytics |
| **Certificate Hash** | SHA1 thumbprint | Network logs | SSL inspection |
| **YARA Rule** | Pattern matching rule | EDR, AV scan | YARA engine |

## IOC Confidence Levels

| Level | Meaning | Action |
|-------|---------|--------|
| High | Seen in multiple threat intel sources | Block immediately |
| Medium | Suspicious, limited corroboration | Alert and investigate |
| Low | Single source, possible FP | Monitor only |
| Unknown | No intel available | Investigate manually |

## IOC Sharing Platforms

| Platform | Type | Link |
|----------|------|------|
| MISP | Open source threat intel platform | [misp-project.org](https://www.misp-project.org) |
| AlienVault OTX | Free community threat intel | [otx.alienvault.com](https://otx.alienvault.com) |
| Abuse.ch | Malware/botnet tracking | [abuse.ch](https://abuse.ch) |
| URLhaus | Malware URL database | [urlhaus.abuse.ch](https://urlhaus.abuse.ch) |
| FeodoTracker | C2 IP tracking | [feodotracker.abuse.ch](https://feodotracker.abuse.ch) |
