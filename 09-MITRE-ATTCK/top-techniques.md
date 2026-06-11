# Top 20 ATT&CK Techniques — Know These

Based on real-world prevalence in SOC environments.

| Rank | Technique | ID | Tactic | Why Common |
|------|-----------|-----|--------|-----------|
| 1 | Phishing | T1566 | Initial Access | Easiest way in — human vulnerability |
| 2 | PowerShell | T1059.001 | Execution | Built into Windows, hard to block |
| 3 | Valid Accounts | T1078 | Multiple | Credentials everywhere after breaches |
| 4 | Scheduled Task | T1053.005 | Persistence | Easy, legitimate-looking persistence |
| 5 | LSASS Memory | T1003.001 | Cred Access | All Windows creds accessible here |
| 6 | Obfuscated Files | T1027 | Defense Evasion | Evade AV/SIEM signature detection |
| 7 | Registry Run Keys | T1547.001 | Persistence | Classic, still very common |
| 8 | Pass the Hash | T1550.002 | Lateral Movement | Reuse stolen NTLM hashes |
| 9 | Ingress Tool Transfer | T1105 | C2 | Download further tools post-access |
| 10 | Masquerading | T1036 | Defense Evasion | Name malware like legit processes |
| 11 | Web Protocols C2 | T1071.001 | C2 | HTTP/S blends with normal traffic |
| 12 | Exfil Over C2 | T1041 | Exfiltration | Use same channel for data theft |
| 13 | Windows Command Shell | T1059.003 | Execution | cmd.exe — universally available |
| 14 | Clear Event Logs | T1070.001 | Defense Evasion | Anti-forensics |
| 15 | RDP | T1021.001 | Lateral Movement | Legitimate protocol, hard to block |
| 16 | Kerberoasting | T1558.003 | Cred Access | Crack service account passwords |
| 17 | System Info Discovery | T1082 | Discovery | Attacker maps environment |
| 18 | Account Discovery | T1087 | Discovery | Find users, groups to target |
| 19 | Network Share Discovery | T1135 | Discovery | Find data to steal |
| 20 | Data Encrypted (Ransomware) | T1486 | Impact | Monetize the compromise |
