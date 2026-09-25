# 🐍 Project 06 — Windows Log Analyser (Python)

> 🔲 **Status: Planned** — not built yet.

## Goal
A Python script that reads Windows Event Log CSV exports, flags suspicious patterns and prints a triage summary — automating the first pass a Tier 1 analyst does by hand.

## Planned detections
| Detection | Event ID | Log |
|---|---|---|
| Brute force: 10+ failed logons in 1 hour | 4625 | Security |
| Failures followed by a successful logon | 4625 → 4624 | Security |
| New user account created | 4720 | Security |
| User added to admin group | 4728 / 4732 | Security |
| Suspicious PowerShell command line | 4688 | Security |
| New scheduled task | 4698 | Security |
| New service installed | 7045 | **System** (separate export) |

## Planned approach
1. Export Security and System logs from Event Viewer as CSV
2. Load with `pandas`
3. Filter by Event ID, group by user/IP, count per hour
4. Flag anything over threshold, with a severity level
5. Print a summary report

## Test data
Will be generated in the [home lab](../02-soc-homelab/) so the output shows real detections, not made-up ones.
