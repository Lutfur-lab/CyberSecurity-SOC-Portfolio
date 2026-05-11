# 🕵️ Project 05 — Threat Intelligence Report: Emotet

## What is this?
A professional threat intelligence report on Emotet malware, written exactly like a real SOC analyst would produce. Includes IOCs, MITRE ATT&CK mapping, and detection recommendations.

## Why employers love this
Writing a real threat intel report shows you can think strategically. It demonstrates MITRE ATT&CK knowledge, research skills, and professional writing — all valued in SOC and cloud security roles.

## Report Contents

### Executive Summary
Emotet is a modular banking trojan turned malware distribution platform. First observed 2014, it is distributed primarily via phishing emails with malicious Office attachments and remains one of the most prevalent threats to UK organisations.

### MITRE ATT&CK Mapping
| Tactic | Technique | ID |
|--------|-----------|-----|
| Initial Access | Phishing attachment | T1566.001 |
| Execution | Malicious macro (Office) | T1204.002 |
| Persistence | Scheduled Task | T1053.005 |
| C2 | Encrypted channel | T1573 |
| Lateral Movement | Pass the Hash | T1550.002 |

### IOC Types to collect
- File hashes (MD5, SHA256)
- C2 IP addresses and domains
- Email sender domains
- Subject line patterns
- Attachment names

### Detection Recommendations (Sentinel KQL)
```kql
SecurityEvent
| where EventID == 4688
| where ParentProcessName has "WINWORD.EXE"
| where NewProcessName has_any ("powershell.exe","cmd.exe","wscript.exe")
| project TimeGenerated, Computer, Account, CommandLine
```

### Sources used
- attack.mitre.org
- app.any.run
- bazaar.abuse.ch
- cisa.gov

## Skills shown
Threat intelligence · MITRE ATT&CK · IOC analysis · Detection engineering · Research
