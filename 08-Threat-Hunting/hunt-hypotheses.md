# Threat Hunt Hypothesis Library

> A library of ready-to-use hunt hypotheses mapped to ATT&CK.

## Persistence Hunts

| # | Hypothesis | ATT&CK | Data Source |
|---|-----------|--------|-------------|
| H01 | Attackers created scheduled tasks for persistence outside normal deployment windows | T1053.005 | Windows 4698, Sysmon |
| H02 | Malicious services installed to maintain access | T1543.003 | Windows 7045 |
| H03 | Registry run keys modified to execute malware on startup | T1547.001 | Sysmon 13 |
| H04 | New local admin accounts created by non-admin users | T1136.001 | Windows 4720, 4732 |

## Execution Hunts

| # | Hypothesis | ATT&CK | Data Source |
|---|-----------|--------|-------------|
| H05 | PowerShell used to download and execute payloads from internet | T1059.001 | Windows 4688, Sysmon 1 |
| H06 | Office applications spawning command shell processes (macro malware) | T1566.001 | Sysmon 1 |
| H07 | Living-off-the-land binaries (LOLBins) used for execution | T1218 | Windows 4688 |
| H08 | Encoded/obfuscated command lines to evade detection | T1027 | Windows 4688, PS 4104 |

## Lateral Movement Hunts

| # | Hypothesis | ATT&CK | Data Source |
|---|-----------|--------|-------------|
| H09 | PsExec or similar tools used for lateral movement | T1021.002 | Windows 7045, 4624 Type 3 |
| H10 | WMI used for remote code execution | T1021.006 | Sysmon 1, Windows 4688 |
| H11 | Pass-the-hash: network logons from unexpected sources | T1550.002 | Windows 4624 Type 3 |
| H12 | RDP lateral movement to servers by workstations | T1021.001 | Windows 4624 Type 10 |

## C2 / Exfiltration Hunts

| # | Hypothesis | ATT&CK | Data Source |
|---|-----------|--------|-------------|
| H13 | Regular outbound connections at fixed intervals (beaconing) | T1071 | Firewall, proxy, DNS logs |
| H14 | DNS tunneling for C2 communication | T1071.004 | DNS logs |
| H15 | Unusually large outbound data transfers | T1041 | Firewall, proxy logs |
| H16 | Connections to Tor exit nodes or known VPN services | T1090 | Firewall logs |

## Credential Access Hunts

| # | Hypothesis | ATT&CK | Data Source |
|---|-----------|--------|-------------|
| H17 | LSASS memory accessed by non-system processes | T1003.001 | Sysmon 10 |
| H18 | Credential dumping tools executed (Mimikatz, procdump) | T1003 | Windows 4688, Sysmon 1 |
| H19 | Kerberoasting: many service ticket requests from single account | T1558.003 | Windows 4769 |
