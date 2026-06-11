# Phishing Incident Playbook

**Incident Type:** Phishing Email  
**Severity:** P3 (Medium) — escalate to P2 if user clicked

---

## Step 1: Initial Triage (L1 — 15 minutes)

- [ ] Obtain the suspicious email (forward as attachment, preserve headers)
- [ ] Identify: Did the user click any links? Open attachments?
- [ ] Check email headers (MXToolbox, original sender IP)
- [ ] Analyze URLs: URLScan.io, VirusTotal
- [ ] Analyze attachments (if any): VirusTotal hash lookup, Any.run sandbox
- [ ] Determine: Phishing attempt (no click) or Compromise (clicked)?

**If user did NOT click/open:** → Proceed to Step 4 (document and block)  
**If user DID click/open:** → Proceed to Step 2 (escalate immediately)

---

## Step 2: Escalation & Scope (L1 escalates to L2)

- [ ] Escalate to L2 with all evidence gathered so far
- [ ] Check: Was the email sent to multiple users? (mass phishing)
- [ ] Pull EDR/SIEM data on affected user's endpoint
- [ ] Look for: New processes, outbound connections, file drops after click time

---

## Step 3: Containment (L2)

- [ ] Isolate affected endpoint if compromise confirmed
- [ ] Disable compromised user account
- [ ] Block malicious domain/URL/IP at perimeter firewall/proxy
- [ ] Pull and quarantine all copies of the phishing email from all mailboxes

---

## Step 4: Eradication & Documentation (L1/L2)

- [ ] Remove quarantined emails
- [ ] Add sender domain to email block list
- [ ] Add malicious URLs/IPs to proxy/firewall blocklist
- [ ] Add file hashes to AV/EDR block list
- [ ] Document all IOCs (sender, URLs, IPs, hashes)

---

## Step 5: Recovery

- [ ] Re-enable user account after password reset + MFA confirmed
- [ ] Restore endpoint from backup if compromised
- [ ] Notify user with security awareness reminder

---

## IOCs to Document

```
Sender Email:    [attacker@domain.com]
Sender IP:       [IP from email header]
Subject Line:    [Phishing subject]
Malicious URL:   [URL in email]
Attachment Hash: [MD5/SHA256 if applicable]
C2 IP:           [If user clicked and malware called home]
```

---

## Email Header Analysis

```bash
# Key headers to examine:
From:             (can be spoofed)
Return-Path:      (actual reply address)
Received:         (trace the path — read bottom to top)
X-Originating-IP: (source IP of sender)
DKIM-Signature:   (email integrity — did it really come from this domain?)
SPF:              (is sender authorized to send for this domain?)
DMARC:            (pass/fail policy)

# Tools:
MXToolbox:   https://mxtoolbox.com/EmailHeaders.aspx
Mailheader:  https://mailheader.org
```
