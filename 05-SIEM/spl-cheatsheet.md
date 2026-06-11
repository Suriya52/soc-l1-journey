# Splunk SPL Cheat Sheet

## Basic Search Syntax

```spl
index=* "search term"                          # Search all indexes
index=windows sourcetype=WinEventLog           # Specific index + sourcetype
index=main earliest=-24h latest=now            # Time range
index=main earliest=-1h@h latest=@h            # Last full hour

| head 10                                      # First 10 results
| tail 10                                      # Last 10 results
| reverse                                      # Reverse order
```

## Filtering & Fields

```spl
# Field-based filtering
index=windows EventCode=4625

# Multiple values
index=windows (EventCode=4624 OR EventCode=4625)

# NOT operator
index=windows EventCode=4688 NOT CommandLine="*svchost*"

# Wildcard
index=windows CommandLine="*powershell*"

# Field extraction
| fields EventCode, AccountName, IpAddress       # Keep only these fields
| fields - _raw                                  # Remove raw field
| rename AccountName as Username                 # Rename a field
```

## Statistics Commands

```spl
# Count events
index=windows EventCode=4625 | stats count

# Count by field
index=windows EventCode=4625 | stats count by src_ip

# Multiple aggregations
index=windows | stats count, avg(duration), max(duration) by host

# Top values
index=windows EventCode=4688 | top NewProcessName limit=20

# Rare values
index=windows | rare CommandLine limit=10

# Time-based bucketing
index=windows EventCode=4625
| timechart span=1h count by src_ip

# Table output
index=windows EventCode=4624
| stats count by AccountName, LogonType, IpAddress
| sort -count
| table AccountName, LogonType, IpAddress, count
```

## SOC Detection Queries

```spl
# Brute force detection (5+ failures in 5 minutes)
index=windows EventCode=4625
| bucket _time span=5m
| stats count by _time, src_ip, TargetUserName
| where count >= 5
| sort -count

# Brute force followed by success
index=windows (EventCode=4625 OR EventCode=4624)
| stats count(eval(EventCode=4625)) as failures,
        count(eval(EventCode=4624)) as successes by src_ip
| where failures > 5 AND successes > 0

# PowerShell with encoded command
index=windows EventCode=4688
| where like(CommandLine, "%-EncodedCommand%")
    OR like(CommandLine, "%-enc %")
    OR like(CommandLine, "%-e %")

# New local admin account created
index=windows EventCode=4720
| join AccountName [search index=windows EventCode=4732
    | rename MemberName as AccountName]

# Cleared event logs
index=windows EventCode=1102
| table _time, host, SubjectUserName

# Scheduled task created
index=windows EventCode=4698
| table _time, host, SubjectUserName, TaskName, TaskContent

# Lateral movement via network logon
index=windows EventCode=4624 LogonType=3
| stats count by AccountName, IpAddress
| where count > 10
| sort -count
```

## Useful SPL Functions

```spl
# Convert epoch timestamp
| eval readable_time=strftime(_time, "%Y-%m-%d %H:%M:%S")

# String operations
| eval domain=lower(AccountName)
| eval length=len(CommandLine)

# Conditional
| eval alert_level=if(count>100, "HIGH", if(count>50, "MEDIUM", "LOW"))

# Extract from regex
| rex field=CommandLine "(?i)(?P<encoded_cmd>(?:[A-Za-z0-9+/]{4})*(?:[A-Za-z0-9+/]{2}==|[A-Za-z0-9+/]{3}=))"

# Decode base64
| eval decoded=base64decode(encoded_cmd)
```
