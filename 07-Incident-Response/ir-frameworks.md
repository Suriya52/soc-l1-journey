# Incident Response Frameworks

## NIST SP 800-61 vs SANS PICERL

| Phase | NIST SP 800-61 | SANS PICERL |
|-------|---------------|-------------|
| 1 | Preparation | Preparation |
| 2 | Detection & Analysis | Identification |
| 3 | Containment | Containment |
| 4 | Eradication | Eradication |
| 5 | Recovery | Recovery |
| 6 | Post-Incident Activity | Lessons Learned |

## NIST Phases in Detail

### Phase 1: Preparation
- IR policy and plan documented
- IR team trained and on-call roster set
- Tools available (forensic workstation, jump bag)
- Communication channels established
- Playbooks written for known incident types
- SIEM, EDR, logging configured

### Phase 2: Detection & Analysis
- Monitor SIEM, EDR, IDS alerts
- Receive reports from users, helpdesk
- Triage to determine if it's a real incident
- Assess scope: what systems, users, data?
- Prioritize by severity and business impact
- Document everything from this point on

### Phase 3: Containment
**Short-term containment:** Stop the bleeding immediately
- Isolate affected systems from network
- Block malicious IP at firewall
- Disable compromised accounts
- Preserve evidence before any changes

**Long-term containment:**
- Apply emergency patches
- Change all potentially compromised passwords
- Deploy additional monitoring

### Phase 4: Eradication
- Remove malware from affected systems
- Delete attacker accounts, backdoors, scheduled tasks
- Patch the exploited vulnerability
- Rebuild systems if necessary

### Phase 5: Recovery
- Restore from clean backup or rebuild
- Re-enable systems and accounts
- Monitor closely for 30+ days post-incident
- Validate that the threat is gone

### Phase 6: Post-Incident Activity
- Write lessons learned report
- Update playbooks based on what happened
- Tune detection rules to catch this faster next time
- Management briefing
