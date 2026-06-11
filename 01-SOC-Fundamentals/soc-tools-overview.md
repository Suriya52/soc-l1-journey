# SOC Tools Overview

> Know the toolset before you sit down at the analyst's desk.

## Tool Categories in a SOC

```
DATA COLLECTION          DETECTION              RESPONSE
──────────────           ─────────              ────────
Syslog / Agents    →     SIEM           →       SOAR
EDR Sensors        →     IDS/IPS        →       Ticketing
Network Taps       →     DLP            →       Forensics Tools
Cloud Logs         →     Threat Intel   →       Communication
```

---

## SIEM (Security Information & Event Management)

The SOC analyst's primary workspace. Collects, normalizes, and correlates logs from all sources.

| Tool | Type | Used For |
|------|------|----------|
| **Splunk** | Commercial | Enterprise SIEM, SPL query language |
| **IBM QRadar** | Commercial | Enterprise SIEM, large environments |
| **Microsoft Sentinel** | Cloud (Azure) | Cloud-native SIEM, KQL queries |
| **ELK Stack** | Open Source | Elasticsearch + Logstash + Kibana |
| **Wazuh** | Open Source | SIEM + EDR + log analysis |
| **AWS CloudWatch + GuardDuty** | Cloud (AWS) | Cloud-native monitoring (Suriya has this!) |

---

## EDR (Endpoint Detection & Response)

Monitors endpoint activity in real-time — processes, files, network connections, registry.

| Tool | Vendor |
|------|--------|
| CrowdStrike Falcon | CrowdStrike |
| Microsoft Defender for Endpoint | Microsoft |
| SentinelOne | SentinelOne |
| Carbon Black | VMware |
| Wazuh | Open Source |

---

## Network Security Monitoring

| Tool | Purpose |
|------|---------|
| **Wireshark** | Packet capture and analysis |
| **Zeek (Bro)** | Network traffic analysis / log generation |
| **Suricata** | IDS/IPS — signature and anomaly detection |
| **Snort** | Classic IDS/IPS |
| **NetworkMiner** | Network forensics, file extraction |

---

## Threat Intelligence

| Tool | Purpose |
|------|---------|
| **VirusTotal** | File/URL/IP/domain reputation |
| **MISP** | Threat intel platform — IOC sharing |
| **AbuseIPDB** | IP reputation database |
| **URLScan.io** | URL and webpage analysis |
| **Shodan** | Internet-facing asset search |
| **AlienVault OTX** | Open threat intelligence community |

---

## SOAR (Security Orchestration, Automation & Response)

Automates repetitive SOC tasks and orchestrates response workflows.

| Tool | Vendor |
|------|--------|
| Splunk SOAR (Phantom) | Splunk |
| Palo Alto XSOAR | Palo Alto Networks |
| TheHive | Open Source |
| IBM Resilient | IBM |

---

## Case Management / Ticketing

| Tool | Purpose |
|------|---------|
| **TheHive** | Open source incident case management |
| **ServiceNow** | Enterprise ITSM with security module |
| **Jira** | Often used in smaller SOC teams |
| **PagerDuty** | Alert routing and on-call management |

---

## Malware Analysis

| Tool | Purpose |
|------|---------|
| **Any.run** | Interactive online malware sandbox |
| **VirusTotal** | Multi-engine static analysis |
| **Cuckoo Sandbox** | Open source automated sandbox |
| **PEStudio** | Static PE file analysis |
| **Volatility** | Memory forensics |

---

## Web Application Security (Relevant for Suriya)

| Tool | Purpose |
|------|---------|
| **Burp Suite** | Web proxy, payload analysis, interception |
| **OWASP ZAP** | Open source web app scanner |
| **Nikto** | Web server vulnerability scanner |

---

## AWS Security Tools (Suriya's Existing Skillset)

| Tool | SOC Function |
|------|-------------|
| **CloudTrail** | Log source — API activity |
| **CloudWatch** | SIEM-style alerting and dashboards |
| **GuardDuty** | Threat detection (ML-based) |
| **AWS Security Hub** | Aggregated security findings |
| **AWS Config** | Configuration compliance monitoring |
| **IAM Access Analyzer** | Detect over-permissioned resources |

---

## Tool Priority for Suriya (Learning Order)

```
ALREADY HAVE ──── AWS CloudTrail, CloudWatch, GuardDuty
                  Burp Suite, Wireshark, Nmap, Metasploit

LEARN NEXT   ──── Splunk (most common enterprise SIEM)
                  ELK Stack (open source, home lab friendly)
                  Wazuh (free SIEM + EDR for home lab)

THEN         ──── TheHive (case management)
                  Sigma (detection rules)
                  Velociraptor (threat hunting)
```
