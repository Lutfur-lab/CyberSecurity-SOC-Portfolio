# 🐍 Project 06 — Windows Log Analyser (Python)

## What is this?
A Python script that reads Windows Event Log CSV exports, identifies suspicious patterns automatically, and outputs a threat summary report. Automates what a Tier 1 analyst does manually.

## Why employers love this
Python scripting is increasingly expected in SOC roles. A working script that solves a real analyst problem shows initiative, technical ability, and understanding of SOC workflows — rare at entry level.

## What it detects
- Brute force: 5+ failed logins (Event 4625) in 1 hour
- New user accounts created (Event 4720)
- Suspicious PowerShell commands (Event 4688)
- New scheduled tasks (Event 4698)
- New services installed (Event 7045)

## Sample output
```
===== LOG ANALYSIS REPORT =====
File: windows_events.csv  |  Total events: 4,821

[CRITICAL] BRUTE FORCE DETECTED
  Account: administrator | Failures: 47 | Source: 192.168.1.105

[HIGH] NEW USER ACCOUNT CREATED
  Account: backdoor_user | Created by: SYSTEM | Time: 03:42:11

[HIGH] SUSPICIOUS POWERSHELL
  User: john.smith | Command: powershell.exe -enc SQBFAFgA...

VERDICT: CRITICAL — Escalate immediately
================================
```

## How to build it
1. Export Windows Event Logs from Event Viewer as CSV
2. Load with Python pandas
3. Filter rows by EventID
4. Group by user/IP, count failures per hour
5. Flag anything over threshold
6. Print summary report

## Skills shown
Python · Pandas · Log analysis · Windows Event IDs · SOC automation
