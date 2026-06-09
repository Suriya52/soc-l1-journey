# 📋 06 — Log Analysis

> Logs are the breadcrumbs attackers leave behind. Learn to read them.

## Purpose
Log analysis is the day-to-day work of a SOC analyst. This section covers how to read, parse, correlate, and extract meaning from different log types.

## Topics Covered

- [ ] Log types: Windows Event Logs, Syslog, Web logs, Firewall logs
- [ ] Log parsing and field extraction
- [ ] Log correlation across sources
- [ ] Baseline vs anomaly identification
- [ ] Common attack patterns in logs
- [ ] Apache/Nginx web server log analysis
- [ ] DNS log analysis
- [ ] Authentication log analysis
- [ ] Firewall and network device logs
- [ ] Endpoint Detection & Response (EDR) logs

## Files in This Folder

| File | Description |
|------|-------------|
| `windows-log-analysis.md` | Windows Security event log guide |
| `linux-log-analysis.md` | Linux syslog and auth log guide |
| `web-log-analysis.md` | Apache/Nginx log analysis |
| `firewall-log-analysis.md` | Firewall and network log analysis |
| `dns-log-analysis.md` | DNS query log investigation |
| `log-correlation-techniques.md` | Multi-source correlation methods |

## Log Analysis Methodology

```
1. IDENTIFY    → What log source? What time range?
2. FILTER      → Narrow to relevant events
3. CORRELATE   → Link events across sources/time
4. BASELINE    → Is this normal behavior?
5. INVESTIGATE → Follow the thread
6. DOCUMENT    → Record findings with evidence
```

## Suspicious Patterns to Hunt

### Authentication Logs
- Multiple failed logins followed by a success (brute force → compromise)
- Login at unusual hours (2–4 AM)
- Login from a new geographic location
- Service account logging in interactively

### Process Logs
- `cmd.exe` or `powershell.exe` spawned by `Office` apps
- Base64 encoded PowerShell commands
- `whoami`, `net user`, `ipconfig` executed in sequence
- LOLBins: `certutil`, `bitsadmin`, `mshta`, `regsvr32`

### Network Logs
- Connections to known-bad IPs/domains
- Beaconing pattern (regular intervals to same destination)
- Large outbound data transfers
- DNS queries to newly registered domains
