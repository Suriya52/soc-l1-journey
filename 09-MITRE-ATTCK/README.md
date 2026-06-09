# ⚔️ 09 — MITRE ATT&CK

> The universal language of adversary behavior.

## Purpose
MITRE ATT&CK is the industry-standard framework for describing attacker tactics, techniques, and procedures (TTPs). Every SOC analyst must be fluent in it.

## Topics Covered

- [ ] ATT&CK framework structure (Tactics → Techniques → Sub-techniques)
- [ ] Enterprise ATT&CK matrix
- [ ] All 14 tactics explained
- [ ] Top 20 most common techniques
- [ ] Mapping alerts to ATT&CK TTPs
- [ ] Using ATT&CK Navigator
- [ ] ATT&CK for detection coverage mapping

## Files in This Folder

| File | Description |
|------|-------------|
| `attack-framework-overview.md` | Full framework explanation |
| `tactics-guide.md` | All 14 tactics with examples |
| `top-techniques.md` | Most commonly seen techniques |
| `detection-mappings.md` | Technique → detection rule mappings |
| `attack-navigator-notes.md` | Using ATT&CK Navigator |

## The 14 ATT&CK Tactics

| # | Tactic | ID | Description |
|---|--------|-----|-------------|
| 1 | Reconnaissance | TA0043 | Gathering info before the attack |
| 2 | Resource Development | TA0042 | Building attack infrastructure |
| 3 | Initial Access | TA0001 | Getting a foothold |
| 4 | Execution | TA0002 | Running malicious code |
| 5 | Persistence | TA0003 | Maintaining access after reboot |
| 6 | Privilege Escalation | TA0004 | Getting higher permissions |
| 7 | Defense Evasion | TA0005 | Avoiding detection |
| 8 | Credential Access | TA0006 | Stealing credentials |
| 9 | Discovery | TA0007 | Learning the environment |
| 10 | Lateral Movement | TA0008 | Moving to other systems |
| 11 | Collection | TA0009 | Gathering data to exfiltrate |
| 12 | Command & Control | TA0011 | Communication with implants |
| 13 | Exfiltration | TA0010 | Stealing data out |
| 14 | Impact | TA0040 | Disrupting/destroying systems |

## Most Common Techniques (Know These Cold)

| Technique | ID | Tactic | Detection |
|-----------|-----|--------|-----------|
| Phishing | T1566 | Initial Access | Email gateway, sandbox |
| PowerShell | T1059.001 | Execution | Process creation logs |
| Scheduled Task | T1053.005 | Persistence | Event ID 4698 |
| Credential Dumping (LSASS) | T1003.001 | Cred Access | Event ID 10 (Sysmon) |
| Pass the Hash | T1550.002 | Lateral Movement | Event ID 4624 Type 3 |
| Obfuscated Files | T1027 | Defense Evasion | Command line analysis |
