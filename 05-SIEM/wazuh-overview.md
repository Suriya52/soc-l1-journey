# Wazuh Overview for SOC Analysts

## What is Wazuh?

Wazuh is a free, open-source SIEM + EDR platform. It's ideal for home labs and smaller organizations. Wazuh provides:
- Log data analysis
- Intrusion detection
- File integrity monitoring (FIM)
- Vulnerability detection
- Configuration assessment

## Architecture

```
Wazuh Agents (endpoints)
        │
        │ (encrypted, compressed)
        ▼
Wazuh Manager (analysis engine)
        │
        ▼
Elasticsearch (data storage)
        │
        ▼
Kibana + Wazuh Dashboard (visualization)
```

## Key Wazuh Rule Groups

| Rule Group | Description |
|-----------|-------------|
| syslog | Linux system log events |
| windows | Windows Event Log events |
| web | Web server (Apache/Nginx) |
| sshd | SSH authentication events |
| su, sudo | Privilege escalation |
| authentication_failed | Failed login events |
| authentication_success | Successful logins |
| pci_dss, gdpr | Compliance mapping |

## Wazuh Alert Levels

| Level | Meaning | Example |
|-------|---------|---------|
| 0–3 | Informational | Normal activity |
| 4–7 | Low concern | Minor policy violation |
| 8–11 | Medium concern | Suspicious activity |
| 12–14 | High concern | Attack indicators |
| 15 | Critical | Active compromise |

## Home Lab Setup

```bash
# Install Wazuh all-in-one (manager + indexer + dashboard)
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash ./wazuh-install.sh -a

# Default dashboard: https://localhost
# Default credentials in /var/log/wazuh-install.log
```
