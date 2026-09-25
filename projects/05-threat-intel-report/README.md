# 🕵️ Project 05 — Threat Intelligence Profile: Emotet

> 🟡 **Status: In progress** — IOC section still to be populated.

## Executive Summary
Emotet began in 2014 as a banking trojan and evolved into a malware distribution platform, selling access to infected machines to other criminal groups (including ransomware operators). It spreads mainly through phishing emails with malicious Office documents or links.

Its infrastructure was taken down in a Europol-led operation in January 2021. It re-emerged in late 2021, and activity since has been **intermittent** — bursts of spam campaigns followed by long quiet periods. It remains relevant as a case study in how loaders operate, even when not currently active.

## MITRE ATT&CK Mapping (Emotet — S0367)
| Tactic | Technique | ID |
|---|---|---|
| Initial Access | Spearphishing Attachment | T1566.001 |
| Initial Access | Spearphishing Link | T1566.002 |
| Execution | User Execution: Malicious File | T1204.002 |
| Execution | PowerShell | T1059.001 |
| Persistence | Registry Run Keys | T1547.001 |
| Persistence | Windows Service | T1543.003 |
| Credential Access | Brute Force: Password Guessing | T1110.001 |
| Lateral Movement | SMB/Windows Admin Shares | T1021.002 |
| Collection | Local Email Collection | T1114.001 |
| Command & Control | Web Protocols | T1071.001 |

*Verify against the current Emotet entry at attack.mitre.org before relying on this list.*

## Indicators of Compromise
> 🔲 To populate from **MalwareBazaar** (tag: `Emotet`) and **ThreatFox**, with dates — IOCs go stale fast, so every entry needs a first-seen date.

| Type | Value | First seen | Source |
|---|---|---|---|
| — | — | — | — |

## Detection (Sentinel KQL)
Office application spawning a script interpreter — classic macro-based execution:
```kql
SecurityEvent
| where EventID == 4688
| where ParentProcessName has_any ("WINWORD.EXE", "EXCEL.EXE")
| where NewProcessName has_any ("powershell.exe", "cmd.exe", "wscript.exe", "cscript.exe", "mshta.exe")
| project TimeGenerated, Computer, Account, ParentProcessName, NewProcessName, CommandLine
```

## Defensive Recommendations
- Block macros in Office files from the internet (default in modern Microsoft 365 — verify it's enforced)
- Alert on Office → script interpreter process chains (query above)
- Restrict SMB between workstations to limit lateral spread
- Strong local admin passwords (LAPS) to defeat password-guessing spread

## Sources
- MITRE ATT&CK — Emotet (S0367)
- Europol — January 2021 Emotet takedown announcement
- CISA — Emotet advisories
- abuse.ch — MalwareBazaar / ThreatFox
