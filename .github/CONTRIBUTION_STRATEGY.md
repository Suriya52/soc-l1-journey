# 🟩 GitHub Contribution Strategy

> How to build a green, recruiter-impressive GitHub profile while learning SOC.

---

## 🎯 The Goal

Every green square in your GitHub contribution graph is proof of consistency. Recruiters and hiring managers **do** look at this. A year of consistent commits tells a story better than any cover letter.

---

## 📅 Daily Commit Routine (15–60 min)

Even on busy days, do ONE of these:

| Task | Time | Commit Message |
|------|------|---------------|
| Add today's daily log | 5 min | `📅 daily: [date] learning log` |
| Add a cheatsheet entry | 10 min | `📚 learn: Add [topic] notes to [module]` |
| Complete a lab step | 20 min | `🧪 lab: [lab name] step X complete` |
| Fix/improve existing notes | 10 min | `✏️ fix: Improve [topic] documentation` |
| Add a tool command | 5 min | `🛠️ tool: Add [tool] command to cheatsheet` |

---

## 🗂️ Repository Setup Instructions

### Step 1: Create the Repository

```bash
# On GitHub.com:
# 1. Click "New repository"
# 2. Name: soc-l1-journey
# 3. Visibility: Public (portfolios need to be visible!)
# 4. Initialize with README: No (we have our own)
# 5. Click "Create repository"
```

### Step 2: Clone and Push

```bash
# Clone your new repo
git clone https://github.com/YOUR_USERNAME/soc-l1-journey.git
cd soc-l1-journey

# Copy all files from this structure
# Then:
git add .
git commit -m "🎉 init: Initialize SOC L1 learning journey portfolio"
git push origin main
```

### Step 3: Set Up Branch Strategy

```bash
# Work on a daily branch, merge to main
git checkout -b learning/week-01
# ... do your work ...
git add .
git commit -m "📚 learn: Complete networking OSI model notes"
git push origin learning/week-01
# Create PR and merge to main on GitHub
```

---

## 🏷️ Commit Message Convention

Follow this emoji + type prefix system:

```
📚 learn:   New notes or study content
🧪 lab:     Lab walkthrough or exercise
🚩 ctf:     CTF challenge writeup
🛠️ tool:   Security tool documentation  
📋 ir:      Incident response content
🔍 hunt:    Threat hunting content
🎯 mitre:   MITRE ATT&CK content
📅 daily:   Daily learning log
📊 week:    Weekly progress report
🏗️ struct:  Repository structure changes
✏️ fix:     Fix typos or improve notes
🚀 project: Project documentation
📜 cert:    Certification study content
```

**Examples:**
```
📚 learn: Add Splunk SPL query cheatsheet
🧪 lab:   Complete TryHackMe Wireshark basics lab
🚩 ctf:   Add CyberDefenders OpenVPN writeup
📅 daily: June 5 — Covered TCP/IP and DNS
📊 week:  Week 23 progress report — 12hrs logged
```

---

## 📌 GitHub Profile README

> Create a separate repo named `YOUR_USERNAME/YOUR_USERNAME` with a README.md to display on your GitHub profile. Include:

```markdown
## 👋 Hi, I'm [Name] | Aspiring SOC Analyst

🛡️ Currently learning: SOC Level 1 | Blue Team Security
📚 Studying: CompTIA Security+ | TryHackMe SOC Path
🔭 Building: My SOC L1 portfolio → [soc-l1-journey](link)
📍 Location: [City, Country]
💬 Ask me about: Log analysis, SIEM, Incident Response

### 🧰 Tools I'm Learning
![Splunk](badge) ![Linux](badge) ![Wireshark](badge) ![Python](badge)
```

---

## 📊 GitHub Actions: Auto-Update Progress

Create `.github/workflows/update-readme.yml` to auto-update your last-commit date in README:

```yaml
name: Update README timestamp

on:
  push:
    branches: [ main ]

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Update last updated badge
        run: |
          DATE=$(date +'%B %d, %Y')
          sed -i "s/Last%20Updated-.*-blue/Last%20Updated-${DATE// /%20}-blue/" README.md
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add README.md
          git diff --staged --quiet || git commit -m "🤖 auto: Update last-modified date"
          git push
```

---

## 🔖 GitHub Topics to Add

On your repo, click the gear ⚙️ next to "About" and add these topics:

```
soc cybersecurity blue-team siem splunk incident-response
threat-hunting mitre-attack log-analysis ctf-writeups
security-operations learning-journey portfolio
```

This makes your repo discoverable by recruiters and other learners.

---

## 📋 Issue Templates

Use GitHub Issues to track your learning tasks:

### Bug/Gap Template
```markdown
**Module:** 05-SIEM
**Gap Identified:** I don't understand Splunk index management
**Resources to check:** [Splunk docs link]
**Status:** Open
```

### Learning Goal Template  
```markdown
**Goal:** Complete ELK Stack home lab setup
**Target Date:** YYYY-MM-DD
**Success Criteria:** Can ingest and query Windows logs in Kibana
**Status:** In Progress
```

---

## ⭐ How to Get Stars & Visibility

1. **Share on LinkedIn** — Post weekly progress updates with a link
2. **Share on Twitter/X** — Use `#100DaysOfCyber`, `#SOC`, `#BlueTeam`
3. **Post on Reddit** — r/cybersecurity, r/netsec, r/blueteamsec
4. **Link in TryHackMe/HTB profile** 
5. **Add to your resume** immediately — "Actively documented on GitHub"

---

*[← Back to Main](../README.md)*
