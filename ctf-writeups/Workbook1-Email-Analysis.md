# Workbook 1 — Email Analysis
**Alert Type:** External Email With Script or Binary Attachment  
**Platform:** TryHackMe  
**Date Completed:** May 2026  
**Difficulty:** L1 SOC Analyst Level  

---

## Scenario
Investigated a suspicious external email containing a script 
or binary attachment. Followed a structured SOC workbook to 
triage the alert and determine if the attachment was malicious.

---

## Steps I Followed

### Step 1 — Took Ownership of the Alert
- Used identity inventory to gather context on email recipients
- Identified who received the email inside the organisation

### Step 2 — Email Investigation
- Analysed the email using EML analyser
- Checked SPF and DKIM authentication results
- Reviewed sender domain reputation
- Examined email content for social engineering indicators

### Step 3 — Recipient Login Investigation
- Investigated login events for all email recipients
- Checked access to corporate servers
- Reviewed VPN login activity for anomalies

### Step 4 — Attachment Analysis
- Used sandbox environment to detonate binary attachments
- Performed manual code review for script attachments
- Looked for indicators of compromise (IOCs)

---

## Decision Point
**Is the attachment malicious, origin faked, or email suspicious?**

- If YES → Gathered triage evidence and escalated to L2 analyst
- If NO → Wrote alert comment confirming email was safe and expected

---

## Tools Used
| Tool | Purpose |
|---|---|
| EML Analyser | SPF/DKIM checks, sender reputation |
| Sandbox | Safe detonation of binary files |
| Identity Inventory | Recipient context |
| SIEM | Login event investigation |

---

## What I Learned
- How SPF and DKIM failures can indicate email spoofing
- Why checking recipient context matters before escalating
- How to safely analyse attachments without infecting systems
- How to structure evidence before handing off to L2
- Importance of notifying employees during active investigation

---

## Outcome
Alert triaged successfully following structured L1 workbook.  
Evidence gathered and verdict documented before any escalation decision.
