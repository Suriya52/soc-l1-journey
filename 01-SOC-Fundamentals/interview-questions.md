# SOC L1 Interview Questions & Answers

> Study these. Real interview questions with strong answers.

---

## Fundamentals

**Q1: What is the difference between a security event and a security incident?**

> An **event** is any observable occurrence in a system or network — a login, a file access, a network connection. Most events are completely normal. An **incident** is an event (or series of events) that negatively impacts the confidentiality, integrity, or availability of data or systems, or violates security policy. Every incident starts with events, but not every event becomes an incident.

---

**Q2: What is the difference between IDS and IPS?**

> An **IDS (Intrusion Detection System)** monitors network traffic and generates alerts when suspicious patterns are found — it detects but takes no action. An **IPS (Intrusion Prevention System)** sits inline in the network and can actively block or drop malicious traffic in real time. In a SOC, IDS/IPS alerts feed into the SIEM for analyst review.

---

**Q3: What are the phases of incident response?**

> The **NIST SP 800-61** framework defines four phases:
> 1. **Preparation** — policies, tools, training in place before incidents occur
> 2. **Detection & Analysis** — identify and investigate the incident
> 3. **Containment, Eradication & Recovery** — stop the threat, remove it, restore systems
> 4. **Post-Incident Activity** — lessons learned, documentation, rule tuning
>
> The **SANS PICERL** model adds Identification and Lessons Learned as explicit steps.

---

**Q4: What is a SIEM and what does it do?**

> A **SIEM (Security Information and Event Management)** platform collects log data from across the entire IT environment — endpoints, servers, network devices, cloud services — normalizes it into a common format, and applies correlation rules to detect suspicious patterns. It's the central nervous system of a SOC. Analysts use it to search logs, investigate alerts, and build dashboards. I have hands-on experience with AWS CloudWatch and GuardDuty as a SIEM-equivalent in cloud environments, and I'm currently learning Splunk.

---

**Q5: What is the MITRE ATT&CK framework?**

> MITRE ATT&CK is a knowledge base of adversary tactics, techniques, and procedures (TTPs) based on real-world threat observations. It's organized into 14 **Tactics** (the "why" — like Initial Access, Persistence, Lateral Movement) and hundreds of **Techniques** (the "how"). SOC analysts use it to describe attacker behavior in incident reports, map detections to known TTPs, and identify coverage gaps. During my Hack The Box work, I practiced identifying kill chain phases like enumeration (Discovery), privilege escalation (Privilege Escalation), and lateral movement.

---

## Technical Questions

**Q6: Walk me through how you would triage a brute force alert.**

> First, I'd review the alert details in the SIEM: which account was targeted, source IP, time window, and number of attempts. I'd check the IP reputation on AbuseIPDB or VirusTotal to see if it's known-malicious. I'd look at whether the attempts succeeded — a successful login after many failures is a red flag. I'd check if the behavior is expected (e.g., an IT admin testing) or anomalous. If it looks like a genuine external brute force, I'd escalate to L2 with all evidence documented, and recommend blocking the source IP at the firewall.

---

**Q7: What are some common Windows Event IDs you should know?**

> The most important ones are:
> - **4624** — Successful logon (baseline and anomaly detection)
> - **4625** — Failed logon (brute force detection)
> - **4672** — Special privileges assigned (admin activity tracking)
> - **4688** — New process created (malware execution detection)
> - **4698** — Scheduled task created (persistence mechanism)
> - **4732** — User added to security group (privilege escalation)
> - **1102** — Audit log cleared (always investigate — attacker anti-forensics)
> - **7045** — New service installed (backdoor/persistence)

---

**Q8: What is the difference between a vulnerability, a threat, and a risk?**

> - A **vulnerability** is a weakness in a system (e.g., unpatched software, misconfigured service)
> - A **threat** is anything that could exploit that vulnerability (e.g., an attacker, malware, insider)
> - A **risk** is the potential impact if the threat exploits the vulnerability — calculated as Likelihood × Impact
>
> Example: An unpatched Apache server (vulnerability) exposed to the internet could be exploited by automated scanners (threat), potentially leading to a full server compromise (risk — high impact, high likelihood).

---

**Q9: What is a false positive and how do you handle it?**

> A false positive is when a security alert fires on legitimate, benign activity. For example, an IT admin running an authorized port scan triggering an IDS alert. When I identify a FP, I document my reasoning clearly in the ticket — what evidence showed it was benign, who the user was, and what they were actually doing. I close the ticket with a FP classification and note whether the detection rule should be tuned to reduce future similar FPs. Reducing FP rate is important to prevent alert fatigue.

---

**Q10: Tell me about a hands-on security project you've done.**

> I configured an AWS security monitoring lab using CloudTrail, CloudWatch, and GuardDuty. I set up metric filters and CloudWatch alarms to alert on root account usage, IAM policy changes, and security group modifications — essentially building a cloud SIEM. I also created an IAM lab where I simulated privilege misuse scenarios and monitored them through CloudTrail logs. Additionally, I completed 50+ PortSwigger labs on OWASP Top 10 vulnerabilities using Burp Suite, which helped me understand the attack payloads I'll see in real SOC alert queues.

---

## Behavioral Questions

**Q11: How do you prioritize when you have multiple alerts in your queue?**

> I prioritize by severity first — Critical and High alerts before Medium and Low. Within the same severity, I look at the affected asset: a domain controller alert takes priority over a workstation. I also consider time sensitivity — an active brute force in progress is more urgent than a historical anomaly. I always communicate with my team lead if the queue is overwhelming so we can allocate resources appropriately.

**Q12: What would you do if you suspected a colleague was the insider threat?**

> I would not confront the colleague directly or take unilateral action. I would document the suspicious behavior with evidence, follow the organization's incident response and HR policy for insider threat investigations, and escalate to my SOC manager or security leadership confidentially. Insider threat investigations require careful handling to preserve evidence and avoid tipping off the subject.
