# Top Ports & Services Reference

## Critical Ports for SOC (Know These Cold)

| Port | Service | Protocol | Risk Level | Notes |
|------|---------|----------|------------|-------|
| 21 | FTP | TCP | 🔴 High | Cleartext creds — always alert |
| 22 | SSH | TCP | 🟡 Medium | Brute force target |
| 23 | Telnet | TCP | 🔴 Critical | Unencrypted — should never appear |
| 25 | SMTP | TCP | 🟡 Medium | Spam relay vector |
| 53 | DNS | TCP/UDP | 🟡 Medium | Tunneling, poisoning |
| 80 | HTTP | TCP | 🟡 Medium | Unencrypted web |
| 110 | POP3 | TCP | 🟡 Medium | Email — cleartext |
| 135 | RPC | TCP | 🔴 High | Windows exploitation vector |
| 139 | NetBIOS | TCP | 🔴 High | Legacy Windows file sharing |
| 143 | IMAP | TCP | 🟡 Medium | Email — cleartext |
| 443 | HTTPS | TCP | 🟢 Low | Encrypted web |
| 445 | SMB | TCP | 🔴 Critical | EternalBlue, ransomware propagation |
| 1433 | MSSQL | TCP | 🔴 High | Database — should not be internet-facing |
| 1521 | Oracle DB | TCP | 🔴 High | Database — should not be internet-facing |
| 3306 | MySQL | TCP | 🔴 High | Database — should not be internet-facing |
| 3389 | RDP | TCP | 🔴 Critical | Brute force, BlueKeep exploit |
| 4444 | Metasploit | TCP | 🔴 Critical | Common C2 default — always alert |
| 5985 | WinRM | TCP | 🔴 High | Remote PowerShell, lateral movement |
| 6379 | Redis | TCP | 🔴 High | Often misconfigured, no auth |
| 8080 | HTTP Alt | TCP | 🟡 Medium | Web proxy, dev servers |
| 8443 | HTTPS Alt | TCP | 🟡 Medium | Web app alternate port |
| 27017 | MongoDB | TCP | 🔴 High | Often misconfigured, no auth |

## Alert on These Immediately

```
Port 4444  → Metasploit default listener
Port 1337  → "Leet" port — common in CTFs and some malware
Port 31337 → "Elite" port — classic backdoor
Port 6666/6667 → IRC — old-school C2 communication
Port 9001/9030 → Tor communication
```
