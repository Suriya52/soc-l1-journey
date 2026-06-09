# ⚙️ 10 — Detection Engineering

> Turn knowledge of attacker TTPs into automated detections.

## Purpose
Detection engineering is the practice of creating, testing, and maintaining detection rules. This section covers Sigma rules, YARA, and detection logic design.

## Topics Covered

- [ ] Detection engineering principles
- [ ] Sigma rule syntax and writing
- [ ] YARA rule basics
- [ ] Testing and validating detection rules
- [ ] Rule lifecycle management
- [ ] Reducing false positives
- [ ] Detection-as-code concepts

## Files in This Folder

| File | Description |
|------|-------------|
| `detection-engineering-intro.md` | Core concepts and methodology |
| `sigma-rules/` | Collection of Sigma rules |
| `sigma-rules/rdp-bruteforce.yml` | RDP brute force detection |
| `sigma-rules/powershell-download.yml` | PowerShell download cradle |
| `sigma-rules/mimikatz-detection.yml` | Mimikatz credential dumping |
| `yara-rules/` | YARA rules for malware detection |
| `detection-testing-guide.md` | How to test your rules |

## Sigma Rule Anatomy

```yaml
title: Suspicious PowerShell Download Cradle
id: a8f34d6c-1234-5678-abcd-ef0123456789
status: experimental
description: Detects PowerShell downloading files from the internet
references:
  - https://attack.mitre.org/techniques/T1059/001/
author: Your Name
date: 2024/01/01
tags:
  - attack.execution
  - attack.t1059.001
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    Image|endswith: '\powershell.exe'
    CommandLine|contains:
      - 'DownloadFile'
      - 'DownloadString'
      - 'WebClient'
      - 'IEX'
      - 'Invoke-Expression'
  condition: selection
falsepositives:
  - Legitimate admin scripts
  - Software update mechanisms
level: high
```
