# 🚨 07 — Incident Response

> When the alarm sounds, every minute matters. Know the playbook.

## Purpose
Incident Response (IR) is the structured process for handling security incidents. This section covers the frameworks, playbooks, and documentation skills needed for effective IR.

## Topics Covered

- [ ] IR frameworks: NIST SP 800-61, SANS PICERL
- [ ] IR phases: Preparation, Detection, Containment, Eradication, Recovery
- [ ] Evidence collection and chain of custody
- [ ] Incident classification and severity levels
- [ ] Escalation procedures
- [ ] Playbooks for common incident types
- [ ] Post-incident analysis and lessons learned
- [ ] Communication during incidents

## Files in This Folder

| File | Description |
|------|-------------|
| `ir-frameworks.md` | NIST and SANS IR framework comparison |
| `playbooks/` | Incident-specific response playbooks |
| `playbooks/phishing-playbook.md` | Phishing incident playbook |
| `playbooks/malware-playbook.md` | Malware incident playbook |
| `playbooks/ransomware-playbook.md` | Ransomware response playbook |
| `ir-checklist.md` | Quick-reference IR checklist |
| `severity-classification.md` | Incident severity levels |

## IR Frameworks at a Glance

### NIST SP 800-61 Phases
```
1. PREPARATION      → Policies, tools, training in place
2. DETECTION        → Identify the incident
3. ANALYSIS         → Understand scope and impact
4. CONTAINMENT      → Stop the spread (short & long term)
5. ERADICATION      → Remove the threat
6. RECOVERY         → Restore to normal operations
7. POST-INCIDENT    → Lessons learned, documentation
```

### SANS PICERL
```
P → Preparation
I → Identification
C → Containment
E → Eradication
R → Recovery
L → Lessons Learned
```

## Incident Severity Levels

| Level | Severity | Example | Response Time |
|-------|----------|---------|---------------|
| P1 | Critical | Active ransomware, data breach | Immediate |
| P2 | High | Compromised admin account | < 1 hour |
| P3 | Medium | Malware on single endpoint | < 4 hours |
| P4 | Low | Phishing email, no compromise | < 24 hours |
| P5 | Informational | Policy violation | Next business day |
