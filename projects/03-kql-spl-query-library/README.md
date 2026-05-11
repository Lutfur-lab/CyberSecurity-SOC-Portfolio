# 🔍 Project 03 — KQL & SPL Query Library

## What is this?
A personal library of threat detection queries for Microsoft Sentinel (KQL) and Splunk (SPL). Each query is documented with what it detects, why it matters, and a real-world use case.

## Why employers love this
The SOC Analyst job description you found requires Microsoft Sentinel. Showing real queries puts you ahead of every applicant who only studied theory.

## KQL Queries — Microsoft Sentinel

### Brute force detection
```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogins = count() by Account, IpAddress, bin(TimeGenerated, 1h)
| where FailedLogins > 10
| order by FailedLogins desc
```
Detects: 10+ failed logins in 1 hour from same IP

### New admin account created
```kql
SecurityEvent
| where EventID == 4720
| project TimeGenerated, Account, SubjectUserName, Computer
| order by TimeGenerated desc
```
Detects: New user accounts — common persistence technique

### Suspicious PowerShell
```kql
SecurityEvent
| where EventID == 4688
| where CommandLine has_any ("-enc", "IEX", "DownloadString", "-nop")
| project TimeGenerated, Computer, Account, CommandLine
```
Detects: Encoded PowerShell — used heavily in malware

## SPL Queries — Splunk

### Failed logins over threshold
```spl
index=windows EventCode=4625
| stats count by src_ip, user
| where count > 10
| sort -count
```

### New scheduled tasks
```spl
index=windows EventCode=4698
| table _time, user, TaskName, TaskContent
```

## Skills shown
Microsoft Sentinel · KQL · Splunk · SPL · Threat detection logic
