# Detection Rule Testing Guide

## Why Test?

A rule that fires on everything is useless. A rule that never fires is dangerous. Testing validates that your rule catches the attack AND doesn't flood analysts with noise.

## Testing Methods

### 1. Atomic Red Team (Recommended)

[Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) provides small, atomic tests mapped to ATT&CK techniques you can run in your lab.

```powershell
# Install
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1')
Install-AtomicRedTeam

# Run a specific technique test
Invoke-AtomicTest T1053.005         # Test scheduled task persistence
Invoke-AtomicTest T1059.001         # Test PowerShell execution
Invoke-AtomicTest T1003.001         # Test LSASS dump
```

### 2. Manual Testing

For simple rules, manually simulate the activity:

```powershell
# Test brute force rule (run 6 times with wrong password)
net use \\localhost\IPC$ /user:Administrator wrongpassword

# Test scheduled task rule
schtasks /create /sc minute /mo 1 /tn "TestTask" /tr "cmd.exe /c whoami"

# Test PowerShell encoded command rule
powershell -EncodedCommand ZQBjAGgAbwAgAEgAZQBsAGwAbwA=
```

### 3. PCAP Replay

For network-based rules, replay known-malicious PCAPs in your lab:

```bash
# Replay a PCAP file
tcpreplay -i eth0 malicious_traffic.pcap
```

## Measuring Rule Quality

| Metric | Formula | Target |
|--------|---------|--------|
| True Positive Rate | TPs / (TPs + FNs) | > 90% |
| False Positive Rate | FPs / (FPs + TNs) | < 10% |
| Precision | TPs / (TPs + FPs) | > 85% |
