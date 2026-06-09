# 🔍 Threat Hunting Report

---

## Hunt Information

| Field | Details |
|-------|---------|
| **Hunt ID** | TH-[YYYY]-[NNN] |
| **Title** | [Descriptive hunt title] |
| **Analyst** | [Your Name] |
| **Date** | [YYYY-MM-DD] |
| **Duration** | [X hours] |
| **Data Sources** | [SIEM / EDR / Network logs / etc.] |
| **Outcome** | 🟢 Nothing Found / 🔴 Threat Discovered |

---

## Hypothesis

> *"I believe [attacker action] may be occurring in the environment because [reason/trigger], which would manifest as [observable indicator]."*

**Example:**  
> "I believe threat actors may be using scheduled tasks for persistence because we recently patched a vulnerability that may have been exploited, which would manifest as new scheduled tasks created outside business hours."

---

## Trigger / Motivation

*What prompted this hunt?*

- [ ] Threat intelligence report
- [ ] Recent vulnerability disclosure
- [ ] Anomalous behavior observed
- [ ] Proactive routine hunt
- [ ] Post-incident follow-up
- [ ] Other: [...]

---

## ATT&CK Coverage

| Tactic | Technique | Sub-technique | ID |
|--------|-----------|--------------|-----|
| Persistence | Scheduled Task/Job | Scheduled Task | T1053.005 |
| [Tactic] | [Technique] | [Sub-technique] | [ID] |

---

## Scope

**Time Range:** [Start DateTime] → [End DateTime]  
**Systems in Scope:**  
- [System/subnet/all endpoints]

**Data Sources Used:**

| Source | Location | Volume |
|--------|----------|--------|
| Windows Security Logs | SIEM | [X events] |
| Sysmon Logs | SIEM | [X events] |
| EDR Telemetry | EDR Platform | [X events] |

---

## Hunt Queries

### Query 1: [Description]

**Platform:** Splunk / KQL / osquery  
**Purpose:** [What this query looks for]

```spl
[Paste your query here]
```

**Results:** [X results found]  
**Notable:** [Any interesting results]

---

### Query 2: [Description]

```spl
[Paste your query here]
```

**Results:** [X results found]

---

## Analysis

### Baseline Established

*What does normal look like for this activity?*

> [Describe normal baseline — e.g., "On average, 3–5 scheduled tasks are created per week by the SYSTEM account during business hours"]

### Anomalies Found

| # | Finding | Timestamp | System | User | Suspicious Because |
|---|---------|-----------|--------|------|--------------------|
| 1 | New schtask at 3AM | 2024-01-15 03:14 UTC | WS001 | SYSTEM | Created outside business hours |
| 2 | [Finding] | [Time] | [Host] | [User] | [Reason] |

---

## Findings

### Finding 1 (If Applicable)

- **Title:** [Short descriptive title]
- **Severity:** [Critical / High / Medium / Low / Informational]
- **Description:** [Detailed finding description]
- **Evidence:**
  ```
  [Log snippet or query result]
  ```
- **Assessment:** [Is this malicious, suspicious, or benign?]

---

## IOCs Discovered

| Type | Value | Confidence | Notes |
|------|-------|------------|-------|
| [Type] | [Value] | [High/Med/Low] | [Context] |

> *"None found"* if hunt returned clean results.

---

## Conclusion

**Was the hypothesis confirmed?**  
☐ Yes — Threat activity found  
☐ Partially — Suspicious activity, requires further investigation  
☐ No — No evidence found

**Summary:**
> [2–3 sentences summarizing what was found or not found, and what it means.]

---

## Recommendations

1. **[Recommendation 1]**  
   Priority: High/Medium/Low  
   Action: [What should be done]

2. **Convert Hunt to Detection Rule**  
   *The following Sigma rule was created from this hunt:*
   ```yaml
   # [Sigma rule based on your hunt queries]
   ```

---

## Follow-up Actions

| Action | Owner | Priority | Status |
|--------|-------|----------|--------|
| Create Sigma rule for finding | Analyst | High | ⬜ Open |
| Investigate IOCs further | L2 Analyst | Medium | ⬜ Open |
| Update threat intel platform | TI Team | Low | ⬜ Open |

---

*Hunt Analyst: [Your Name] | Date: [YYYY-MM-DD]*
