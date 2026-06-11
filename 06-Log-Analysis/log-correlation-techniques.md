# Log Correlation Techniques

## What is Log Correlation?

Correlation means connecting events across multiple log sources and time periods to reveal a full attack story that no single log could tell alone.

## The Kill Chain Correlation Model

```
Stage 1: Reconnaissance
    └── Web server logs: scanning activity from 45.33.32.156
                         ↓
Stage 2: Initial Access
    └── Email gateway: phishing email delivered to alice@company.com
                         ↓
Stage 3: Execution
    └── Windows Security (4688): winword.exe → cmd.exe on ALICE-PC
                         ↓
Stage 4: Persistence
    └── Windows Security (4698): New scheduled task created
                         ↓
Stage 5: Lateral Movement
    └── Windows Security (4624 Type 3): Login to FILESERVER from ALICE-PC
                         ↓
Stage 6: Exfiltration
    └── Firewall logs: Large upload from FILESERVER to 45.33.32.156
```

## Correlation Approaches

### Time-Based Correlation
Connect events that happened close together in time.
```
10:30:00 - Phishing email opened (email gateway log)
10:30:15 - Word process spawned cmd.exe (Windows 4688)
10:30:20 - PowerShell download from unknown IP (firewall log)
10:30:25 - New scheduled task created (Windows 4698)
```

### Entity-Based Correlation
Follow a single entity (IP, user, hostname) across all log sources.
```
IP 192.168.1.50:
- Auth log: Successful SSH login at 02:00
- Firewall: Connected to 5 internal hosts at 02:05
- Web log: Accessed /admin panel at 02:10
- SIEM: Triggered 3 alerts in 10 minutes
```

### IOC-Based Correlation
Hunt a known indicator across all sources.
```
IOC: IP 45.33.32.156 (known C2)
├── Firewall logs: Outbound connection from WORKSTATION-07
├── Proxy logs: HTTP GET requests every 60 seconds (beaconing)
├── DNS logs: queries to c2.evil.com (resolves to 45.33.32.156)
└── Windows logs: powershell.exe making the connection (Sysmon Event 3)
```
