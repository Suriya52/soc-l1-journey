# KQL (Kibana Query Language) Cheat Sheet

## Basic Syntax

```kql
# Simple field search
event.code: "4625"

# Multiple values (OR)
event.code: ("4624" or "4625")

# AND condition
event.code: "4688" and process.name: "powershell.exe"

# NOT
event.code: "4688" and not process.name: "svchost.exe"

# Wildcard
process.command_line: "*EncodedCommand*"

# Range
event.code >= 4624 and event.code <= 4625
```

## SOC Detection Queries

```kql
# Failed logins
event.code: "4625"

# Successful logins
event.code: "4624"

# PowerShell execution
event.code: "4688" and process.name: "powershell.exe"

# Encoded PowerShell
event.code: "4688" and process.command_line: "*-EncodedCommand*"

# Scheduled task created
event.code: "4698"

# Cleared event logs
event.code: "1102"

# New service installed
event.code: "7045"

# Network connections from PowerShell (Sysmon)
event.code: "3" and process.name: "powershell.exe"

# LSASS access (credential dumping - Sysmon)
event.code: "10" and winlog.event_data.TargetImage: "*lsass*"

# Outbound connections to suspicious ports
event.code: "3" and destination.port: (4444 or 1337 or 6666)
```

## Kibana Dashboard Tips

- Use **Lens** for quick visualizations
- **TSVB** for time-series analysis
- **Maps** for geolocation of IPs
- **Alerting** to create SIEM-style rules
- **Timeline** for incident investigation
