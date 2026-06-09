# 🔍 Threat Hunt Report

> **Hunt ID:** HUNT-YYYY-XXXX  
> **Copy to `08-Threat-Hunting/hunt-XXX-name.md`**

---

## 📋 Hunt Metadata

| Field | Details |
|-------|---------|
| **Hunt ID** | HUNT-YYYY-XXXX |
| **Hunt Name** | |
| **Analyst** | Your Name |
| **Date Started** | YYYY-MM-DD |
| **Date Completed** | YYYY-MM-DD |
| **Duration** | X hours |
| **Data Sources** | Windows Events / Network Logs / EDR / DNS |
| **Environment** | Home Lab / TryHackMe / LetsDefend |
| **Outcome** | 🟢 Nothing Found / 🔴 Threat Found / 🟡 Suspicious Activity |

---

## 🎯 Hunt Hypothesis

> *"I believe [THREAT ACTOR / TECHNIQUE] is present in this environment because [REASONING]."*

**Hypothesis:**  


**Based on:**
- [ ] Threat intelligence report
- [ ] Recent vulnerability disclosure  
- [ ] Observed anomaly
- [ ] MITRE ATT&CK technique
- [ ] Other: ___

---

## 🔭 Hunt Scope

**Time Range:** YYYY-MM-DD to YYYY-MM-DD  
**Systems in Scope:**  
**Data Sources Used:**

| Source | Type | Coverage |
|--------|------|----------|
| Windows Security Events | Log | Full |
| Sysmon | Telemetry | Full |
| Network Flows | NetFlow | Partial |
| DNS Logs | Log | Full |

---

## 🎯 MITRE ATT&CK Techniques Hunted

| Technique | Sub-Technique | Description |
|-----------|---------------|-------------|
| T1059.001 | PowerShell | Malicious PowerShell execution |
| | | |

---

## 🔍 Hunt Methodology

**Approach used:**
- [ ] TTP-based (hunting for known attacker behavior)
- [ ] IOC-based (hunting for specific indicators)
- [ ] Anomaly-based (hunting for outliers)
- [ ] Hypothesis-driven

**Kill Chain / ATT&CK stage focused:**  

---

## 📊 Hunt Queries

### Query 1 — [Description]

**Tool:** Splunk / ELK / KQL  
**Purpose:**  

```splunk
index=windows source="WinEventLog:Security"
EventCode=4104
| search ScriptBlockText="*Invoke-Expression*" OR ScriptBlockText="*IEX*"
| table _time, host, user, ScriptBlockText
| sort -_time
```

**Results:** X events found  
**Verdict:** Suspicious / Benign / Confirmed Malicious

---

### Query 2 — [Description]

```splunk
# Query here
```

**Results:**  
**Verdict:**

---

## 🔬 Analysis Findings

### Finding 1: [Finding Name]

**Observed:**  
**Why it's notable:**  
**Investigation:**  
**Verdict:** True Positive / False Positive / Benign  

**Evidence:**
```
[Paste relevant log entry or output]
```

---

## 🔴 Confirmed Threats / Suspicious Activity

| # | Finding | Severity | Technique | Recommended Action |
|---|---------|----------|-----------|-------------------|
| 1 | | High | T1xxx | Create detection rule |
| 2 | | Medium | T1xxx | Monitor |

---

## 🟢 False Positives Identified

| # | Activity | Reason Benign | Action |
|---|----------|--------------|--------|
| 1 | | | Tune rule |

---

## 📈 Detection Opportunities

*Based on this hunt, new detection rules I should create:*

| Detection | Query Needed | Priority |
|-----------|-------------|----------|
| | | High/Med/Low |

---

## 📌 Lessons Learned

**What worked well in this hunt:**  

**What I'd do differently next time:**  

**New skills/techniques learned:**  

---

## 📄 Summary & Conclusion

**Hypothesis confirmed?** Yes / No / Partially  

**Overall findings:**  

**Recommended next hunt hypothesis:**  

---

## 🔗 References

- Threat intelligence used:
- MITRE ATT&CK pages:
- Tooling documentation:

---

**Hunt completed by:** [Your Name]  

*[← Threat Hunting](./README.md) | [← Main](../README.md)*
