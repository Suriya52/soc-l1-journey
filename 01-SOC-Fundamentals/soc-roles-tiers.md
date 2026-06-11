# SOC Roles & Tiers

## SOC Tier Structure

```
┌─────────────────────────────────────────────────┐
│              TIER 4 — SOC MANAGER               │
│  Strategy, budgets, reporting, team leadership  │
├─────────────────────────────────────────────────┤
│          TIER 3 — THREAT HUNTER / SME           │
│  Proactive hunting, advanced malware analysis,  │
│  threat intelligence, red team collaboration    │
├─────────────────────────────────────────────────┤
│         TIER 2 — INCIDENT RESPONDER             │
│  Deep-dive investigations, containment,         │
│  forensics, escalation handling                 │
├─────────────────────────────────────────────────┤
│          TIER 1 — ALERT ANALYST (YOU)           │
│  Alert triage, initial investigation,           │
│  escalation to T2, ticket management            │
└─────────────────────────────────────────────────┘
```

## Tier 1 — Alert Analyst (SOC L1)

**That's you. Know this role cold.**

### Responsibilities
- Monitor SIEM dashboards and alert queues 24/7
- Perform initial triage on all incoming alerts
- Classify: True Positive, False Positive, or Benign
- Gather context and evidence for each alert
- Escalate confirmed incidents to Tier 2
- Create and manage tickets in case management system
- Follow runbooks and playbooks for known alert types
- Document all actions taken

### Required Skills
| Skill | Why It Matters |
|-------|---------------|
| SIEM navigation | Your primary workspace |
| Log reading | Raw evidence for every alert |
| Basic networking | Understand traffic context |
| Windows Event IDs | 70% of enterprise alerts |
| Alert triage workflow | Core daily function |
| Communication | Escalation and documentation |

### A Day in the Life of a SOC L1
```
08:00  Shift handover — review overnight alerts
08:30  Begin working alert queue (oldest first)
09:00  Alert: Failed logins — triage → FP (developer testing)
09:30  Alert: Suspicious PowerShell — escalate to T2
10:00  Document findings, close FP tickets
10:30  Proactive log review — nothing suspicious
...
16:00  Shift handover — brief incoming analyst
```

---

## Tier 2 — Incident Responder

### Responsibilities
- Receive escalations from Tier 1
- Conduct deep-dive forensic investigations
- Perform containment and eradication actions
- Analyze malware samples (basic static/dynamic)
- Coordinate with IT teams for remediation
- Write detailed incident reports

---

## Tier 3 — Threat Hunter / SME

### Responsibilities
- Proactively hunt for threats not caught by automated rules
- Develop new detection logic and Sigma rules
- Analyze threat intelligence feeds
- Red team collaboration and purple teaming
- Mentor Tier 1 and Tier 2 analysts

---

## Tier 4 — SOC Manager

### Responsibilities
- Manage analyst team, schedules, and performance
- Report security posture to leadership
- Manage tool budget and vendor relationships
- Define SOC strategy, policies, and processes

---

## Other Roles in the SOC Ecosystem

| Role | Function |
|------|----------|
| Threat Intelligence Analyst | Tracks threat actors, feeds IOCs into SIEM |
| Malware Analyst | Reverse engineers malicious code |
| Forensics Analyst | Evidence collection and analysis |
| Vulnerability Analyst | Scans and tracks vulnerabilities |
| Security Engineer | Maintains and tunes security tools |

---

## Career Progression Path

```
SOC L1 Analyst
    │  (6–18 months experience)
    ▼
SOC L2 Incident Responder
    │  (1–2 years + certs: CySA+, BTL1)
    ▼
SOC L3 Threat Hunter / Senior Analyst
    │  (2–4 years + certs: GCIH, GCFA)
    ▼
SOC Manager / Security Architect / Pen Tester
```

> **Suriya's Path:** SOC L1 → L2 IR → specialize in Cloud Security (AWS) given existing GuardDuty/CloudTrail experience
