# 📋 Project 04 — Incident Response Playbooks (Tier 1)

Playbooks written from a **Tier 1 analyst's** point of view: triage, severity, contain what Tier 1 is allowed to, collect evidence, escalate.

Structure follows NIST SP 800-61: Detect & Analyse → Contain → Eradicate → Recover → Lessons Learned.

---

## 01 — Phishing
| Step | Action |
|---|---|
| 1. Trigger | User report or email security alert |
| 2. Triage (≤15 min) | Check headers (SPF/DKIM/DMARC, Reply-To), URLs, attachments (hash, don't open) |
| 3. Severity | **Low:** no clicks · **Medium:** clicked, no credentials entered · **High:** credentials entered or attachment executed |
| 4. Scope | Search mail logs for the same sender/subject/URL across all mailboxes |
| 5. Contain | Quarantine/purge the email, block sender domain and URL |
| 6. Investigate | Did anyone click? Check proxy/DNS logs and endpoint logs for affected users |
| 7. Escalate | **High** → Tier 2 with IOCs and timeline |
| 8. Recover | Password reset + session revoke for anyone who entered credentials |
| 9. Document | Ticket with IOCs, affected users, actions taken |
| 10. Lessons learned | Tune filters, awareness message to staff |

## 02 — Ransomware
| Step | Action |
|---|---|
| 1. Trigger | EDR/SIEM alert: mass file modification, ransom note, shadow copy deletion |
| 2. Severity | **Critical** by default |
| 3. Contain | Isolate affected hosts (EDR network isolation) — **do not power off**, memory holds evidence |
| 4. Escalate | Immediately to Tier 2 / IR lead — ransomware is not handled solo |
| 5. Preserve evidence | Ransom note, sample hashes, affected file list, memory capture if tooling allows |
| 6. Scope | Find patient zero and entry point; check for other hosts contacting the same C2 |
| 7. Eradicate | *(IR team)* rebuild from known-good images after evidence is collected |
| 8. Recover | *(IR team)* restore from clean, tested backups |
| 9. Document | Full timeline |
| 10. Lessons learned | Backup testing, patch gaps, initial access vector |

> Decisions on ransom payment, legal and regulatory notification (e.g. ICO within 72 hours for personal data breaches) sit with management and legal — not the SOC.

## 03 — Brute Force / Account Compromise
| Step | Action |
|---|---|
| 1. Trigger | 10+ failed logons in 1 hour (see [Project 03](../03-kql-spl-query-library/)) |
| 2. Triage | Internal or external IP? Known scanner? One account or many (spraying)? |
| 3. Key check | **Was there a successful logon (4624) after the failures?** |
| 4. Severity | **Low:** failures only · **High:** failures followed by success |
| 5. Contain | Block source IP; if success → disable account, revoke sessions |
| 6. Escalate | Successful logon → Tier 2 |
| 7. Recover | Password reset, enforce MFA |
| 8. Document | Source IP, timeline, affected accounts |
| 9. Lessons learned | Lockout policy, MFA coverage, exposed services |

## 04 — Malware on Endpoint
> 🔲 Planned
