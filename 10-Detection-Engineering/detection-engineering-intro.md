# Detection Engineering Introduction

## What is Detection Engineering?

Detection engineering is the discipline of creating, testing, maintaining, and improving detection rules that identify malicious activity. It bridges threat intelligence, SOC operations, and tool management.

## Detection Rule Lifecycle

```
THREAT INTEL / HUNT FINDING
           │
           ▼
    HYPOTHESIS
    "How would this TTP appear in logs?"
           │
           ▼
    BUILD THE RULE
    (Sigma, SPL, KQL, YARA)
           │
           ▼
    TEST IN LAB
    Simulate the attack, confirm rule fires
           │
           ▼
    VALIDATE & TUNE
    Check for false positives, adjust thresholds
           │
           ▼
    DEPLOY TO PRODUCTION
    SIEM/EDR active detection
           │
           ▼
    MONITOR & MAINTAIN
    Track FP rate, update as attacker TTPs evolve
```

## Detection Frameworks

### Pyramid of Pain (David Bianco)

```
┌──────────────────────────────────────────────────┐
│          TTPs — Hardest for attacker to change   │  Highest Value
├──────────────────────────────────────────────────┤
│              Tools (malware names, tool versions) │
├──────────────────────────────────────────────────┤
│            Network/Host Artifacts (registry keys) │
├──────────────────────────────────────────────────┤
│                  Domain Names                     │
├──────────────────────────────────────────────────┤
│                    IP Addresses                   │
├──────────────────────────────────────────────────┤
│             Hash Values — Trivial to change       │  Lowest Value
└──────────────────────────────────────────────────┘
```

**Key Insight:** Detect TTPs, not just hashes. A hash changes with every malware recompile. TTPs stay consistent across an attacker's campaigns.

## Writing Effective Detection Rules

### Good Rule Checklist
- [ ] Tied to a specific ATT&CK technique
- [ ] Low false positive rate
- [ ] Tested against real attack data
- [ ] Has documented false positive exceptions
- [ ] Has severity level assigned
- [ ] Reviewed and approved before production
- [ ] Tagged with MITRE ATT&CK ID

### Common Rule Mistakes
- Too broad (matches everything)
- Too narrow (only catches one hash/IP)
- Not tested in lab environment
- No false positive analysis done
- Detects the tool, not the behavior
