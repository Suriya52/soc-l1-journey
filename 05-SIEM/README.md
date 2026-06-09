# 📊 05 — SIEM

> Your primary weapon in the SOC — learn to wield it well.

## Purpose
SIEM (Security Information and Event Management) is the core platform SOC analysts use daily. This section covers Splunk, ELK Stack, and Wazuh — the three most common SIEMs you'll encounter.

## Sub-folders

```
05-SIEM/
├── splunk/
│   ├── README.md
│   ├── spl-cheatsheet.md
│   ├── splunk-queries.md
│   └── dashboards/
├── elk-stack/
│   ├── README.md
│   ├── kql-cheatsheet.md
│   └── elk-setup-notes.md
└── wazuh/
    ├── README.md
    └── wazuh-rules.md
```

## Topics Covered

- [ ] SIEM architecture and data flow
- [ ] Log ingestion and normalization
- [ ] Splunk: SPL (Search Processing Language)
- [ ] Splunk: Creating alerts and dashboards
- [ ] ELK Stack: Elasticsearch, Logstash, Kibana
- [ ] Wazuh: Open-source SIEM/EDR
- [ ] Correlation rules and detection logic
- [ ] SIEM tuning to reduce false positives
- [ ] Creating custom dashboards

## Splunk SPL Quick Reference

```spl
# Basic search
index=windows sourcetype=WinEventLog EventCode=4625

# Count failed logins by source IP
index=windows EventCode=4625 | stats count by src_ip | sort -count

# Top 10 processes by count
index=windows EventCode=4688 | top NewProcessName limit=10

# Time-based search (last 24h)
index=* earliest=-24h latest=now

# Alert: Potential brute force (>5 failures in 5 min)
index=windows EventCode=4625
| bucket _time span=5m
| stats count by _time, src_ip
| where count > 5
```

## ELK KQL Quick Reference

```kql
# Failed logins
event.code: "4625"

# Specific user activity
winlog.event_data.SubjectUserName: "admin" AND event.code: "4624"

# Process creation
event.code: "4688" AND process.name: "powershell.exe"

# Network connections from PowerShell
event.code: "3" AND process.name: "powershell.exe"
```
