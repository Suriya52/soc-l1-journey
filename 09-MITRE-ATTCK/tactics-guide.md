# MITRE ATT&CK Tactics Guide

## All 14 Tactics Explained

### TA0001 — Initial Access
*How attackers get their first foothold in your environment.*

| Technique | ID | Common Example |
|-----------|-----|----------------|
| Phishing | T1566 | Malicious email with attachment |
| Exploit Public-Facing App | T1190 | SQL injection on web app |
| Valid Accounts | T1078 | Credential stuffing against VPN |
| External Remote Services | T1133 | RDP brute force |
| Supply Chain Compromise | T1195 | Malicious software update |

---

### TA0002 — Execution
*How attackers run their malicious code.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| PowerShell | T1059.001 | Event 4688, ScriptBlock log |
| Windows Command Shell | T1059.003 | Event 4688, parent process |
| Scheduled Task/Job | T1053.005 | Event 4698 |
| Windows Management Instrumentation | T1047 | Event 4688, WmiPrvSE |
| User Execution | T1204 | User opened malicious file |

---

### TA0003 — Persistence
*How attackers survive reboots and maintain access.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Scheduled Task | T1053.005 | Event 4698 |
| Registry Run Keys | T1547.001 | Sysmon Event 13 |
| Create Account | T1136 | Event 4720 |
| New Service | T1543.003 | Event 7045 |
| Boot/Logon Autostart | T1547 | Startup folder monitoring |

---

### TA0004 — Privilege Escalation
*How attackers gain higher privileges.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Valid Accounts | T1078 | Event 4672 (special privileges) |
| Exploitation for Privilege Escalation | T1068 | Unusual process spawning as SYSTEM |
| Bypass User Account Control | T1548.002 | High-integrity process from medium-integrity |
| Access Token Manipulation | T1134 | Event 4624 with unusual token |

---

### TA0005 — Defense Evasion
*How attackers hide their activities.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Clear Windows Event Logs | T1070.001 | Event 1102 |
| Obfuscated Files/Info | T1027 | Encoded commands, packed binaries |
| Masquerading | T1036 | Processes named like system processes |
| Disable Security Tools | T1562 | AV/EDR process termination |
| Rootkit | T1014 | Kernel-level anomalies |

---

### TA0006 — Credential Access
*How attackers steal credentials.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| LSASS Memory Dump | T1003.001 | Sysmon Event 10 (LSASS access) |
| Credential in Files | T1552.001 | File access to credentials.txt, web.config |
| Kerberoasting | T1558.003 | Many Event 4769 requests |
| Brute Force | T1110 | Many Event 4625 failures |
| Mimikatz | T1003 | "sekurlsa" in command line |

---

### TA0007 — Discovery
*How attackers learn about your environment.*

| Technique | ID | Command Signature |
|-----------|-----|-------------------|
| Network Share Discovery | T1135 | `net share`, `net view` |
| Account Discovery | T1087 | `net user`, `net localgroup` |
| System Info Discovery | T1082 | `systeminfo`, `hostname` |
| Network Scanning | T1046 | nmap, port scans |
| Process Discovery | T1057 | `tasklist`, `ps` |

**Tip:** A sequence of discovery commands in a short window = attacker mapping your environment.

---

### TA0008 — Lateral Movement
*How attackers move from system to system.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Pass the Hash | T1550.002 | Event 4624 Type 3, NtLmSsp |
| PsExec | T1021.002 | Service PSEXESVC, Event 7045 |
| RDP | T1021.001 | Event 4624 Type 10 |
| WMI | T1021.006 | WmiPrvSE spawning processes |
| SSH | T1021.004 | SSH lateral movement in Linux |

---

### TA0009 — Collection
*How attackers gather data to steal.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Data from Local System | T1005 | Bulk file access events |
| Email Collection | T1114 | Outlook/Exchange data access |
| Clipboard Data | T1115 | Clipboard monitoring tool |
| Screen Capture | T1113 | Unusual screenshot tools |
| Keylogging | T1056.001 | EDR hooks detection |

---

### TA0011 — Command and Control
*How attackers communicate with compromised systems.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Web Protocols (HTTP/S) | T1071.001 | Beaconing pattern, unusual user agents |
| DNS | T1071.004 | Long DNS queries, DNS tunneling |
| Encrypted Channel | T1573 | TLS to uncommon ports |
| Non-Standard Port | T1571 | Common protocols on odd ports |
| Ingress Tool Transfer | T1105 | Downloading tools post-compromise |

---

### TA0010 — Exfiltration
*How attackers steal your data.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Exfil Over C2 Channel | T1041 | Large outbound via C2 connection |
| Exfil Over Web Service | T1567 | Upload to Dropbox, Pastebin, etc. |
| Exfil Over DNS | T1048.003 | DNS with encoded payload in queries |
| Data Transfer Size Limits | T1030 | Many small transfers (avoid detection) |

---

### TA0040 — Impact
*How attackers cause damage.*

| Technique | ID | Detection |
|-----------|-----|-----------|
| Data Encrypted for Impact | T1486 | Ransomware — rapid file encryption |
| Defacement | T1491 | Web content changed |
| Data Destruction | T1485 | Mass file deletion events |
| Service Stop | T1489 | Critical services stopped |
| Account Access Removal | T1531 | Mass account lockout/deletion |
