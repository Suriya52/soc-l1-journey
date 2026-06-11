# Alert Triage Process

> The most critical daily skill for a SOC L1 analyst.

## What is Alert Triage?

Alert triage is the process of reviewing an incoming security alert, gathering context, and deciding whether it represents a real threat (True Positive) or a harmless event (False Positive).

---

## The 6-Step Triage Workflow

```
STEP 1: RECEIVE
    └── Alert appears in SIEM / ticketing queue
         │
STEP 2: REVIEW
    └── Read the alert: What fired? When? Which system? Which user?
         │
STEP 3: GATHER CONTEXT
    └── Pull related logs, check IP reputation, user history
         │
STEP 4: CLASSIFY
    └── True Positive / False Positive / Benign True Positive
         │
STEP 5: ACT
    ├── FP → Document reason, close ticket, consider rule tuning
    └── TP → Escalate to L2, preserve evidence, notify
         │
STEP 6: DOCUMENT
    └── Record every action taken, evidence found, decision made
```

---

## Alert Classification Definitions

| Classification | Definition | Example |
|---------------|------------|---------|
| **True Positive (TP)** | Real attack detected correctly | Actual brute force from external IP |
| **False Positive (FP)** | Benign activity flagged as malicious | IT admin running port scan triggers alert |
| **Benign True Positive (BTP)** | Expected/known activity triggering alert | Scheduled backup triggering anomaly rule |
| **True Negative (TN)** | Normal activity, no alert fired | Regular user login, no alert — correct |
| **False Negative (FN)** | Real attack missed entirely | Attacker uses slow brute force, rule threshold not met |

> **FN is the most dangerous outcome.** Attackers succeed when you miss them.

---

## Context You MUST Gather for Every Alert

### About the Source
- What is the source IP? Is it internal or external?
- IP reputation check (VirusTotal, AbuseIPDB, Shodan)
- Is this IP known-good (e.g., IT admin machine)?
- Geolocation — expected or anomalous?

### About the User
- What user account is involved?
- What is their role? (Admin, developer, standard user?)
- Is this behavior normal for this user?
- Has this user triggered alerts before?

### About the System
- What is the affected system? (Workstation, server, DC?)
- What is its role in the network?
- Is it internet-facing?
- What other activity has this system shown recently?

### About Time
- When did the event occur? Business hours or odd hours?
- Is this a one-time event or a pattern?
- Did anything else happen around the same time?

---

## Triage Cheat Sheet — Common Alert Types

### Brute Force / Failed Logins
```
Questions to ask:
1. How many failures? Over what time window?
2. Was there a successful login after the failures?
3. Is the source IP internal or external?
4. Which account was targeted? Admin? Service account?

TP Indicators:
- 100+ failures from single external IP
- Failures followed by successful login
- Login at 3AM from unknown location

FP Indicators:
- Locked-out user trying to remember password
- Service account with wrong password configured
- IT admin testing from known IP
```

### Suspicious Process Execution
```
Questions to ask:
1. What is the parent process? (Explorer.exe vs Word.exe?)
2. What is the full command line?
3. Is the binary signed by a trusted vendor?
4. Is this process communicating outbound?

TP Indicators:
- cmd.exe spawned by winword.exe (macro malware)
- PowerShell with base64 encoded command
- Process making outbound connection to unknown IP

FP Indicators:
- Known admin tool run by IT team
- Software installer spawning child processes
- Legitimate scripting by developer
```

### Data Exfiltration Alert
```
Questions to ask:
1. How much data? To where?
2. Is the destination IP/domain known?
3. Is this normal for this user/system?
4. What protocol? (HTTP, FTP, DNS tunneling?)

TP Indicators:
- Large upload to unknown external IP
- Transfer at unusual time
- User with no business need for that data

FP Indicators:
- Cloud backup to known provider (OneDrive, S3)
- Developer pushing code to GitHub
- Business-approved file sharing service
```

---

## Escalation Criteria — When to Escalate to L2

Escalate immediately if:
- [ ] Confirmed successful unauthorized access
- [ ] Active malware execution detected
- [ ] Data exfiltration in progress or suspected
- [ ] Compromised privileged/admin account
- [ ] Ransomware indicators (file encryption activity)
- [ ] Multiple systems affected (potential lateral movement)
- [ ] You cannot determine if it's TP or FP after investigation

---

## Documentation Standards

Every triage action must be documented with:

```
Alert ID:     [SIEM alert ID]
Received:     [Timestamp]
Analyst:      [Your name]
Alert Name:   [What fired]
Classification: [TP / FP / BTP]
Evidence:     [Logs, IPs, hashes reviewed]
Actions Taken: [What you did]
Outcome:      [Closed / Escalated / Monitoring]
Time to Close: [Minutes from receive to close]
```
