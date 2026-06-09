# 🚨 Incident Analysis Report

---

## Incident Summary

| Field | Details |
|-------|---------|
| **Incident ID** | IR-[YYYY]-[NNN] |
| **Title** | [Brief incident title] |
| **Date Detected** | [YYYY-MM-DD HH:MM UTC] |
| **Date Reported** | [YYYY-MM-DD HH:MM UTC] |
| **Analyst** | [Your Name] |
| **Severity** | 🔴 Critical / 🟠 High / 🟡 Medium / 🟢 Low |
| **Status** | 🔵 Open / 🟡 Investigating / ✅ Closed |
| **Incident Type** | [Phishing / Malware / Brute Force / Data Breach / etc.] |

---

## Executive Summary

> *2–3 sentences describing what happened, impact, and resolution. Non-technical audience.*

---

## Timeline

| Time (UTC) | Event |
|------------|-------|
| HH:MM | Initial alert triggered in SIEM |
| HH:MM | Alert reviewed by L1 analyst |
| HH:MM | Escalated to L2 — [reason] |
| HH:MM | Containment action taken — [action] |
| HH:MM | Eradication completed |
| HH:MM | Recovery initiated |
| HH:MM | Incident closed |

---

## Detection

**Alert Source:** [SIEM / EDR / IDS / User Report]  
**Alert Name:** [Name of the fired rule/alert]  
**SIEM Query:**
```spl
[Paste the Splunk/KQL query that found the alert]
```

**Initial Indicator:**
> [Describe what the alert showed — e.g., "5 failed login attempts followed by successful login from IP 1.2.3.4"]

---

## Investigation

### Phase 1: Triage

*Was this a True Positive or False Positive?*

- **Verdict:** ✅ True Positive
- **Reasoning:** [Explain why you determined this was real]

### Phase 2: Scope Assessment

**Affected Systems:**

| System | IP Address | Role | Affected? |
|--------|-----------|------|-----------|
| HOSTNAME1 | 10.0.0.5 | Workstation | ✅ Yes |
| HOSTNAME2 | 10.0.0.10 | DC | ❓ Unknown |

**Affected Users:**

| Username | Role | Action Taken |
|----------|------|-------------|
| john.doe | Standard User | Password reset |

### Phase 3: Root Cause Analysis

**How did the attacker gain access?**
> [Describe the initial vector]

**What did the attacker do after gaining access?**
> [Describe attacker actions — lateral movement, data access, etc.]

---

## IOCs

| Type | Value | Confidence | Notes |
|------|-------|------------|-------|
| IP | 1.2.3.4 | High | Source of brute force |
| Email | phish@evil.com | High | Phishing sender |
| Hash (SHA256) | abc...xyz | High | Malware binary |
| Domain | c2.evil.com | Medium | Suspected C2 |
| URL | http://... | High | Malware download |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID | Evidence |
|--------|-----------|-----|---------|
| Initial Access | Phishing | T1566 | Phishing email found in mailbox |
| Execution | PowerShell | T1059.001 | PowerShell command in Event ID 4688 |
| Persistence | Scheduled Task | T1053.005 | Malicious task found in Task Scheduler |

---

## Containment Actions Taken

- [ ] Blocked IP `1.2.3.4` on firewall
- [ ] Isolated host `HOSTNAME1` from network
- [ ] Disabled compromised user account `john.doe`
- [ ] Reset passwords for affected accounts
- [ ] Revoked suspicious active sessions

---

## Eradication

- [ ] Malware removed from endpoint
- [ ] Malicious scheduled task deleted
- [ ] Registry keys cleaned
- [ ] Persistence mechanisms verified removed

---

## Recovery

- [ ] System reimaged / restored from clean backup
- [ ] Accounts re-enabled after password reset
- [ ] Monitoring increased on affected systems
- [ ] Verified clean with AV/EDR scan

---

## Lessons Learned

**What went well:**
- [Point 1]

**What could be improved:**
- [Point 1]

**Recommendations:**
1. [Recommendation 1]
2. [Recommendation 2]

---

## Follow-up Actions

| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| Tune detection rule to reduce FPs | SOC L1 | [Date] | ⬜ Open |
| Patch vulnerable system | IT Team | [Date] | ⬜ Open |
| Security awareness training | HR/Security | [Date] | ⬜ Open |

---

*Report Author: [Your Name] | Created: [Date] | Last Updated: [Date]*
