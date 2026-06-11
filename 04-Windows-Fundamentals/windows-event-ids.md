# Windows Event IDs — Complete SOC Reference

> Print this. Pin it to your monitor. Know these cold.

## Logon & Authentication Events

| Event ID | Description | Why It Matters | Hunt For |
|----------|-------------|----------------|----------|
| **4624** | Successful logon | Baseline activity, detect anomalies | Unusual hours, new IPs |
| **4625** | Failed logon | Brute force detection | >5 failures in 5 min |
| **4634** | Account logoff | Session tracking | — |
| **4647** | User-initiated logoff | — | — |
| **4648** | Logon with explicit credentials | Pass-the-hash, lateral movement | runas, PTH attacks |
| **4672** | Special privileges assigned to logon | Admin activity | Non-admin accounts getting special privs |
| **4768** | Kerberos TGT requested | AD authentication | Failed TGT requests |
| **4769** | Kerberos service ticket requested | Service access | Kerberoasting (many requests) |
| **4771** | Kerberos pre-auth failed | AD brute force | High volume from one IP |
| **4776** | NTLM credential validation | Pass-the-hash indicator | — |

## Logon Types (with 4624/4625)

| Type | Name | Description | Security Note |
|------|------|-------------|---------------|
| 2 | Interactive | Local keyboard login | Normal workstation use |
| 3 | Network | File shares, mapped drives | Lateral movement via SMB |
| 4 | Batch | Scheduled tasks | Check task legitimacy |
| 5 | Service | Service account login | Check service changes |
| 7 | Unlock | Screen unlock | Monitor after hours |
| 10 | RemoteInteractive | RDP session | Brute force target |
| 11 | CachedInteractive | Cached credentials | Offline attack indicator |

## Process & Execution Events

| Event ID | Description | Hunt For |
|----------|-------------|----------|
| **4688** | New process created | cmd/PS spawned by Office, encoded commands |
| **4689** | Process terminated | Short-lived suspicious processes |
| **4657** | Registry value modified | Persistence registry keys |

## Object Access Events

| Event ID | Description | Hunt For |
|----------|-------------|----------|
| **4663** | File object access attempted | Access to sensitive files |
| **4656** | Handle to object requested | Pre-cursor to file access |
| **4660** | Object deleted | Log/evidence deletion |

## Account Management Events

| Event ID | Description | Hunt For |
|----------|-------------|----------|
| **4720** | User account created | Unauthorized account creation |
| **4722** | User account enabled | Re-enabling dormant accounts |
| **4723** | Password change attempt | Self-service password change |
| **4724** | Password reset attempt | Admin password reset |
| **4725** | User account disabled | Account disabling (incident response) |
| **4726** | User account deleted | Account deletion (covering tracks) |
| **4728** | User added to global group | Privilege escalation |
| **4732** | User added to local group | Privilege escalation |
| **4733** | User removed from local group | — |
| **4756** | User added to universal group | — |

## Policy & System Events

| Event ID | Description | Hunt For |
|----------|-------------|----------|
| **1102** | Audit log cleared | ALWAYS INVESTIGATE — attacker anti-forensics |
| **4719** | System audit policy changed | Disabling auditing |
| **4698** | Scheduled task created | Persistence mechanism |
| **4702** | Scheduled task updated | Persistence modification |
| **4699** | Scheduled task deleted | Covering tracks |
| **7045** | New service installed | Malware persistence |
| **7036** | Service started/stopped | Service manipulation |
| **4697** | New service installed (Security log) | Duplicate of 7045 |

## PowerShell Events (Requires ScriptBlock logging)

| Event ID | Log | Description |
|----------|-----|-------------|
| **4103** | PS Operational | Module logging |
| **4104** | PS Operational | ScriptBlock logging — shows full command |
| **400** | PS Operational | Engine started |
| **600** | PS Operational | Provider started |

## Network Events (Sysmon required)

| Sysmon Event | Description |
|-------------|-------------|
| **Event 1** | Process creation (better than 4688) |
| **Event 3** | Network connection (process making outbound) |
| **Event 7** | Image loaded (DLL injection detection) |
| **Event 10** | Process accessed (LSASS access = credential dumping) |
| **Event 11** | File created |
| **Event 13** | Registry value set |
| **Event 22** | DNS query |

## Quick Wins — Queries to Run Daily

```powershell
# All failed logins in last hour
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddHours(-1)}

# All new accounts created today
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4720; StartTime=(Get-Date).Date}

# Audit log cleared
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=1102}

# New services installed
Get-WinEvent -FilterHashtable @{LogName='System'; Id=7045}

# Scheduled tasks created
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4698}
```
