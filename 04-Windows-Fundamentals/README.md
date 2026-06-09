# 🪟 04 — Windows Fundamentals

> Most enterprise environments run Windows. Know it deeply.

## Purpose
Windows is the dominant enterprise OS and the primary target of most attacks. Understanding Windows internals, Active Directory, Event IDs, and PowerShell is essential for SOC analysts.

## Topics Covered

- [ ] Windows architecture overview
- [ ] Active Directory (AD) basics
- [ ] Windows Event Logs and Event IDs
- [ ] Windows Registry for security
- [ ] PowerShell for security analysis
- [ ] Windows authentication (NTLM, Kerberos)
- [ ] User Account Control (UAC)
- [ ] Windows Firewall and Defender
- [ ] Scheduled tasks and persistence mechanisms
- [ ] Common Windows attack techniques

## Files in This Folder

| File | Description |
|------|-------------|
| `windows-event-ids.md` | Critical Event ID reference guide |
| `active-directory-basics.md` | AD concepts for SOC analysts |
| `powershell-for-soc.md` | PowerShell investigation commands |
| `windows-registry-guide.md` | Registry locations for threat hunting |
| `windows-attacks.md` | Common Windows attack techniques |

## 🔑 Critical Windows Event IDs

| Event ID | Description | Why It Matters |
|----------|-------------|----------------|
| 4624 | Successful logon | Baseline and anomaly detection |
| 4625 | Failed logon | Brute force detection |
| 4648 | Logon with explicit credentials | Pass-the-hash, lateral movement |
| 4672 | Special privilege logon | Admin/service account tracking |
| 4688 | New process created | Malware execution, LOLBins |
| 4698 | Scheduled task created | Persistence mechanism |
| 4732 | User added to security group | Privilege escalation |
| 7045 | New service installed | Malware/backdoor persistence |
| 1102 | Audit log cleared | Anti-forensics — always investigate |
| 4776 | NTLM authentication | Pass-the-hash detection |

## PowerShell Investigation Commands

```powershell
# Get recent event logs (last 24 hours)
Get-EventLog -LogName Security -Newest 100 | Where-Object {$_.EventID -eq 4625}

# Check running processes with network connections
Get-NetTCPConnection | Select-Object LocalAddress,LocalPort,RemoteAddress,RemotePort,State,OwningProcess

# Find recently created files
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue | Where-Object {$_.CreationTime -gt (Get-Date).AddDays(-1)}

# List scheduled tasks
Get-ScheduledTask | Where-Object {$_.State -eq "Ready"} | Select-Object TaskName, TaskPath

# Check autorun locations
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
```
