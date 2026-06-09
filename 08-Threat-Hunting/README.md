# 🔍 08 — Threat Hunting

> Don't wait for alerts. Go find the attacker.

## Purpose
Threat hunting is proactive security — searching for threats that evade automated detection. This section covers hunting methodologies, forming hypotheses, and documenting hunts.

## Topics Covered

- [ ] Threat hunting vs reactive monitoring
- [ ] Hypothesis-driven hunting
- [ ] IOC-based vs TTP-based hunting
- [ ] Using MITRE ATT&CK for hunt hypotheses
- [ ] Tools: Velociraptor, osquery, ELK
- [ ] Hunting for common attack patterns
- [ ] Documenting and reporting hunt results

## Files in This Folder

| File | Description |
|------|-------------|
| `hunting-methodology.md` | Frameworks and approaches |
| `hunt-hypotheses.md` | Library of hunting hypotheses |
| `hunt-reports/` | Documented threat hunt reports |
| `hunting-queries.md` | SPL/KQL queries for hunting |

## Hunting Methodology

```
1. HYPOTHESIS    → "Attackers may be using LOLBins for persistence"
2. SCOPE         → Define time range, systems, data sources
3. QUERY         → Build and run detection queries
4. ANALYZE       → Review results for anomalies
5. INVESTIGATE   → Deep-dive into suspicious findings
6. DOCUMENT      → Record findings, IOCs, and TTPs found
7. IMPROVE       → Convert hunt to automated detection rule
```

## Example Hunt Hypotheses

| Hypothesis | ATT&CK TTP | Priority |
|-----------|------------|----------|
| Attackers using scheduled tasks for persistence | T1053.005 | High |
| PowerShell downloading payloads from the internet | T1059.001 | High |
| Lateral movement via PsExec or WMI | T1021 | High |
| C2 beaconing with regular intervals | T1071 | High |
| Credential dumping via LSASS access | T1003.001 | Critical |
