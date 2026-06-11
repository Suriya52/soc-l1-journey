# SOC Metrics & KPIs

> What gets measured gets managed. Know these for interviews.

## Why Metrics Matter

SOC metrics help management understand team performance, justify tool investments, and identify areas for improvement. As an L1 analyst, you'll contribute to these numbers daily.

---

## Core SOC KPIs

### 1. Mean Time to Detect (MTTD)
**Definition:** Average time between when an attack starts and when the SOC detects it.

```
MTTD = Total time from attack start to detection
       ─────────────────────────────────────────
              Number of incidents

Industry average: 197 days (IBM Cost of Data Breach 2023)
Good SOC target:  < 1 hour for critical alerts
```

**What affects it:** SIEM coverage, rule quality, log ingestion speed

---

### 2. Mean Time to Respond (MTTR)
**Definition:** Average time from detection to containment/resolution.

```
MTTR = Total time from detection to resolution
       ───────────────────────────────────────
              Number of incidents

Target: < 4 hours for high severity
        < 24 hours for medium severity
```

**What affects it:** Analyst skill, playbook quality, team size, escalation speed

---

### 3. False Positive Rate
**Definition:** Percentage of alerts that turn out to be non-threatening.

```
FP Rate = False Positives
          ─────────────────── × 100
          Total Alerts Fired

Industry average: 45–80% of alerts are FPs
Target: < 30% (well-tuned SIEM)
```

**Why it matters:** High FP rate causes alert fatigue — analysts stop paying attention

---

### 4. Alert Volume
**Definition:** Total number of alerts generated per day/week/month.

| Metric | Target |
|--------|--------|
| Alerts per analyst per shift | < 50 (manageable) |
| Alerts closed same day | > 90% |
| Backlog (open > 24h) | < 5% |

---

### 5. Mean Time to Triage (MTTT)
**Definition:** How quickly an analyst picks up a new alert from the queue.

```
Target: < 10 minutes for Critical
        < 30 minutes for High
        < 2 hours for Medium
```

---

### 6. Escalation Rate
**Definition:** Percentage of alerts escalated from L1 to L2.

```
Escalation Rate = Alerts escalated to L2
                  ───────────────────────── × 100
                  Total alerts triaged

Healthy range: 5–15%
```

Too high = L1 lacks skill or confidence  
Too low = L1 may be under-escalating real incidents

---

### 7. Alert Dwell Time
**Definition:** How long a threat exists in the environment before being detected and resolved.

```
Short dwell time = effective SOC
Long dwell time  = attackers had time to cause serious damage
```

---

## Metrics Dashboard (What You'll See in a Real SOC)

```
┌────────────────────────────────────────────────────┐
│           SOC OPERATIONS DASHBOARD                 │
├──────────────┬──────────────┬──────────────────────┤
│ Open Alerts  │ Closed Today │ Escalated to L2      │
│     47       │     134      │        8             │
├──────────────┼──────────────┼──────────────────────┤
│  MTTD (avg)  │  MTTR (avg)  │  FP Rate (today)     │
│   18 min     │   2.4 hrs    │      62%             │
├──────────────┴──────────────┴──────────────────────┤
│  CRITICAL: 2  HIGH: 11  MEDIUM: 28  LOW: 6         │
└────────────────────────────────────────────────────┘
```

---

## Interview Tip: Metrics Questions

**Q: "What is MTTD and why does it matter?"**  
A: Mean Time to Detect — the average time between an attack starting and the SOC detecting it. A lower MTTD means less time for attackers to cause damage. It's improved by better detection rules, proper log coverage, and analyst training.

**Q: "What causes alert fatigue and how do you combat it?"**  
A: Alert fatigue occurs when high false positive rates cause analysts to become desensitized to alerts and start ignoring them. You combat it by tuning SIEM rules, creating whitelists for known-good behavior, and regularly reviewing alert quality metrics.
