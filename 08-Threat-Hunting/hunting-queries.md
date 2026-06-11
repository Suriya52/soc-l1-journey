# Threat Hunting Queries

## Splunk SPL Hunting Queries

```spl
─── HUNT: Scheduled Task Persistence ────────────────────────────────
index=windows EventCode=4698
| stats count by SubjectUserName, TaskName, TaskContent, host
| where SubjectUserName != "SYSTEM"
| sort -_time

─── HUNT: PowerShell Download Cradle ────────────────────────────────
index=windows EventCode=4688
| where like(lower(NewProcessName), "%powershell%")
    AND (
        like(CommandLine, "%DownloadFile%")
        OR like(CommandLine, "%DownloadString%")
        OR like(CommandLine, "%WebClient%")
        OR like(CommandLine, "%IEX%")
        OR like(CommandLine, "%Invoke-Expression%")
        OR like(CommandLine, "%-EncodedCommand%")
    )
| table _time, host, SubjectUserName, CommandLine

─── HUNT: Office Apps Spawning Shells ────────────────────────────────
index=windows EventCode=4688
| where (
        like(ParentProcessName, "%WINWORD.EXE%")
        OR like(ParentProcessName, "%EXCEL.EXE%")
        OR like(ParentProcessName, "%OUTLOOK.EXE%")
        OR like(ParentProcessName, "%POWERPNT.EXE%")
    )
    AND (
        like(NewProcessName, "%cmd.exe%")
        OR like(NewProcessName, "%powershell.exe%")
        OR like(NewProcessName, "%wscript.exe%")
        OR like(NewProcessName, "%cscript.exe%")
    )
| table _time, host, SubjectUserName, ParentProcessName, NewProcessName, CommandLine

─── HUNT: Beaconing Detection ────────────────────────────────────────
index=firewall action=allowed
| stats count, avg(bytes_out) as avg_bytes,
        stdev(duration) as stdev_dur,
        dc(_time) as time_slots
    by src_ip, dest_ip, dest_port
| where stdev_dur < 5           /* Regular intervals = low stdev */
    AND time_slots > 10          /* Many connections */
    AND count > 20
| sort stdev_dur

─── HUNT: LSASS Access (Credential Dumping) ──────────────────────────
index=sysmon EventCode=10
| where like(TargetImage, "%lsass.exe%")
    AND NOT (
        like(SourceImage, "%MsMpEng.exe%")
        OR like(SourceImage, "%svchost.exe%")
        OR like(SourceImage, "%csrss.exe%")
        OR like(SourceImage, "%wininit.exe%")
    )
| table _time, host, SourceImage, TargetImage, GrantedAccess
```
