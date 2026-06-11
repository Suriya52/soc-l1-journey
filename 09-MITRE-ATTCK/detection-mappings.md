# ATT&CK Technique → Detection Mapping

> For each technique: what to log, what to query, what to alert on.

| Technique | ID | Log Source | Detection Query (SPL) | Alert Threshold |
|-----------|-----|-----------|----------------------|-----------------|
| Brute Force | T1110 | Windows Security | `EventCode=4625 \| stats count by src_ip \| where count>5` | 5 failures/5min |
| PowerShell | T1059.001 | Windows Security + PS Operational | `EventCode=4688 Image=*powershell* CommandLine=*encoded*` | Any encoded cmd |
| Scheduled Task | T1053.005 | Windows Security | `EventCode=4698 SubjectUserName!=SYSTEM` | Any new task |
| LSASS Dump | T1003.001 | Sysmon | `EventCode=10 TargetImage=*lsass*` | Any non-system access |
| Log Clear | T1070.001 | Windows Security | `EventCode=1102` | Immediate alert |
| New Service | T1543.003 | Windows System | `EventCode=7045` | Any new service |
| Kerberoasting | T1558.003 | Windows Security | `EventCode=4769 \| stats count by AccountName \| where count>20` | Bulk requests |
| Pass the Hash | T1550.002 | Windows Security | `EventCode=4624 LogonType=3 AuthPackage=NTLM` | Unusual source IPs |
| DNS Tunneling | T1071.004 | DNS Logs | `dns.query.name.length>50 \| stats count by client_ip \| where count>100` | High DNS volume |
| Mimikatz | T1003 | Windows Security | `EventCode=4688 CommandLine=*sekurlsa*` | Immediate alert |
