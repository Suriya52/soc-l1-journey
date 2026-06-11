# Threat Hunting Methodology

## What Makes Hunting Different from Monitoring?

| Monitoring | Threat Hunting |
|-----------|---------------|
| Reactive — waits for alerts | Proactive — goes looking |
| Rule-based detection | Hypothesis-driven investigation |
| Catches known patterns | Finds unknown/undetected threats |
| L1 analyst function | L3 analyst / specialist function |
| Alert queue driven | Analyst curiosity driven |

## Hunting Frameworks

### TaHiTI (Targeted Hunting integrating Threat Intelligence)

```
1. INITIATE  → Choose hunting focus (threat intel, recent CVE, internal observation)
2. HUNT      → Create hypothesis, scope, run queries
3. FINALIZE  → Document findings, create detections, update threat intel
```

### PEAK Hunting Framework

```
P → Prepare     (define scope, gather data sources)
E → Execute     (run queries, analyze results)
A → Act         (respond to findings, create detections)
K → Knowledge   (document, share, improve)
```

## Building a Good Hypothesis

**Template:**
> "I believe [attacker action] may be occurring in [scope] because [evidence/trigger], which would appear in the data as [observable indicator]."

**Examples:**

> "I believe attackers may be using scheduled tasks for persistence on Windows endpoints because we recently had a phishing campaign, which would appear as new scheduled tasks created by user accounts rather than SYSTEM, especially outside business hours."

> "I believe there may be active C2 communication because our threat intel feed flagged a related IP, which would appear as regular outbound connections to the same external IP at fixed time intervals (beaconing pattern)."

## Data Sources for Hunting

| Source | What You Find | Tool |
|--------|-------------|------|
| Windows Event Logs | Process creation, logins, policy changes | SIEM |
| Sysmon Logs | Detailed process, network, file, registry | SIEM |
| EDR Telemetry | Endpoint behavior, file changes | EDR platform |
| Network Flow (NetFlow) | Who talked to whom, how much data | SIEM/PCAP |
| DNS Logs | Domain lookups, tunneling, DGA | SIEM |
| Proxy Logs | Web traffic, user agents, categories | SIEM |
| Cloud Logs (CloudTrail) | API activity, IAM changes | AWS/SIEM |
