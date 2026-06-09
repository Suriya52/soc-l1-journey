# 🏢 01 — SOC Fundamentals

> Understanding the heart of defensive security operations.

## Purpose
This section covers the foundational knowledge every SOC analyst needs before touching any tool — what a SOC is, how it functions, the analyst's role, and how alerts flow from detection to resolution.

## Topics Covered

- [ ] What is a SOC? Roles & responsibilities
- [ ] SOC Tier structure (L1 / L2 / L3 / Threat Intelligence)
- [ ] Alert triage process
- [ ] Security monitoring concepts
- [ ] Types of security events vs incidents
- [ ] SIEM role in the SOC
- [ ] Ticketing & case management basics
- [ ] Key SOC metrics (MTTD, MTTR, false positive rate)
- [ ] Shift handover best practices
- [ ] SOC tools landscape overview

## Files in This Folder

| File | Description |
|------|-------------|
| `soc-overview.md` | What a SOC is and how it operates |
| `soc-roles-tiers.md` | Breakdown of SOC roles L1–L4 |
| `alert-triage-process.md` | Step-by-step alert triage workflow |
| `soc-metrics.md` | Key SOC KPIs and what they measure |
| `soc-tools-overview.md` | Common tools used in a SOC |
| `interview-questions.md` | Common SOC L1 interview Q&As |

## Key Concepts

```
Event → Log → Alert → Triage → Investigate → Escalate/Close
```

**True Positive (TP):** Real attack correctly detected  
**False Positive (FP):** Benign activity flagged as malicious  
**True Negative (TN):** Benign activity correctly not flagged  
**False Negative (FN):** Real attack missed — the worst outcome  

## Notes & Insights

> *Add your personal notes, "aha moments", and questions here as you study.*
