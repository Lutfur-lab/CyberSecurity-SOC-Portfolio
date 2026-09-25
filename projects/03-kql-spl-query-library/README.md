# 🔍 Project 03 — KQL & SPL Detection Query Library

> 🟡 **Status: Written, not yet tested** — queries will be validated in the [Sentinel lab](../07-azure-sentinel-lab/) and [home lab](../02-soc-homelab/), with screenshots added.

Detection queries for Microsoft Sentinel (KQL) and Splunk (SPL), each with what it catches and what it misses.

**Standard threshold used across this portfolio:** 10 failed logons in 1 hour.

---

## KQL — Microsoft Sentinel

### 1. Brute force (one account targeted)
```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLogons = count() by TargetAccount, IpAddress, bin(TimeGenerated, 1h)
| where FailedLogons >= 10
| order by FailedLogons desc
```
**Catches:** repeated guesses against one account from one IP.
**Misses:** password spraying (see next query).

### 2. Password spraying (one IP, many accounts)
```kql
SecurityEvent
| where EventID == 4625
| summarize Accounts = dcount(TargetAccount), Attempts = count() by IpAddress, bin(TimeGenerated, 1h)
| where Accounts >= 10
| order by Accounts desc
```
**Catches:** a few guesses each across many accounts — stays under per-account lockout.

### 3. Brute force followed by success
```kql
let failures = SecurityEvent
| where EventID == 4625
| summarize Failures = count() by IpAddress, TargetAccount
| where Failures >= 10;
SecurityEvent
| where EventID == 4624
| join kind=inner failures on IpAddress, TargetAccount
| project TimeGenerated, TargetAccount, IpAddress, Failures, Computer
```
**Why it matters:** failures alone are noise; failures **then a success** means a likely compromise → escalate.

### 4. User added to a privileged group
```kql
SecurityEvent
| where EventID in (4728, 4732, 4756)   // global, local, universal security groups
| where TargetUserName has_any ("Admins", "Administrators")
| project TimeGenerated, Computer, SubjectUserName, MemberName, TargetUserName
```
**Note:** 4720 only means *a user account was created* — it doesn't mean admin. Privilege comes from group membership.

### 5. New user account created
```kql
SecurityEvent
| where EventID == 4720
| project TimeGenerated, Computer, SubjectUserName, TargetUserName
```
**Why it matters:** attacker-created accounts are a common persistence technique (T1136).

### 6. Suspicious PowerShell
```kql
SecurityEvent
| where EventID == 4688
| where NewProcessName endswith "powershell.exe"
| where CommandLine has_any ("-enc", "-EncodedCommand", "IEX", "DownloadString", "-nop", "-w hidden")
| project TimeGenerated, Computer, Account, ParentProcessName, CommandLine
```
**Prerequisite:** "Include command line in process creation events" must be enabled via Group Policy, otherwise `CommandLine` is empty.

---

## SPL — Splunk

### 7. Failed logons over threshold
```spl
index=windows EventCode=4625
| bin _time span=1h
| stats count by _time, src_ip, user
| where count >= 10
| sort -count
```

### 8. Password spraying
```spl
index=windows EventCode=4625
| bin _time span=1h
| stats dc(user) as accounts count as attempts by _time, src_ip
| where accounts >= 10
```

### 9. New scheduled task
```spl
index=windows EventCode=4698
| table _time, host, user, TaskName, TaskContent
```

### 10. DNS exfiltration — unusually long subdomains
*(Built from the [Project 09](../09-dns-exfiltration-investigation/) investigation.)*
```spl
index=* process.name="nslookup.exe"
| rex field=process.command_line "nslookup(?:\.exe)?\s+(?<query>\S+)"
| eval label_len=len(mvindex(split(query,"."),0))
| where label_len > 25
| stats count by host.name, query
```

> Field names (`src_ip`, `user`, `process.name`) depend on how logs are ingested — adjust to your Splunk data model.
