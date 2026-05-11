# 📋 Project 04 — Incident Response Playbooks

## What is this?
Professional IR playbooks for the most common SOC incidents, written as if for use in a real SOC. Covers phishing, ransomware, brute force, and malware.

## Why employers love this
Most candidates know tools. Very few can document a professional process. Writing playbooks shows maturity, communication skills, and deep understanding of SOC operations — valued highly at interview.

## Playbooks

### 01 — Phishing Response
1. TRIGGER: User reports suspicious email or SIEM alert fires
2. TRIAGE: Check headers, URLs, sender IP within 15 mins
3. CONTAIN: Block sender domain, quarantine email
4. INVESTIGATE: Check if user clicked, check endpoint logs
5. ERADICATE: Remove from all mailboxes
6. RECOVER: Reset credentials if compromised
7. DOCUMENT: Full write-up with IOCs
8. LESSONS LEARNED: Update email filters

### 02 — Ransomware Response
1. TRIGGER: SIEM alert for mass file encryption
2. TRIAGE: Identify affected machines immediately
3. CONTAIN: Isolate machines from network NOW
4. INVESTIGATE: Find patient zero, determine entry point
5. ERADICATE: Wipe and rebuild (never pay ransom)
6. RECOVER: Restore from clean backups
7. DOCUMENT: Timeline of events
8. LESSONS LEARNED: Backup review, patch gaps

### 03 — Brute Force / Account Compromise
1. TRIGGER: 10+ failed logins in 1 hour
2. TRIAGE: Is this real or scanner?
3. CONTAIN: Lock account, block source IP
4. INVESTIGATE: Check if any login succeeded
5. ERADICATE: Remove attacker access if compromised
6. RECOVER: Password reset + MFA enforcement
7. DOCUMENT: Source IP, timeline, affected accounts

## Skills shown
Incident response · IR lifecycle · Documentation · SOC process · Risk thinking
