# 🔍 5 Ws Investigation Report — [Alert / Room Name]

---

## 📋 Alert Summary

| Field | Detail |
|-------|--------|
| Date & Time | |
| Alert Name | |
| Severity | Low / Medium / High / Critical |
| Source | TryHackMe / Splunk / Sentinel / Home Lab |
| Analyst | Your name |

---

## 👤 WHO
> Which user, account, or system was involved?

- **Username:**
- **Department / Role:**
- **Is this a privileged account?** Yes / No
- **Normal working hours:** e.g. 09:00–17:00 Mon–Fri
- **Was activity inside normal hours?** Yes / No

---

## ⚡ WHAT
> What exact action or sequence of events happened?

**Event sequence:**
1.
2.
3.

**Commands or processes involved:**
```
paste any commands, scripts, or processes here
```

**Files involved:**
- File name:
- File hash (MD5/SHA256):

**Type of attack (MITRE ATT&CK):**
- Tactic:
- Technique:
- ID: T1xxx

---

## 🕐 WHEN
> Exact timestamps — when did it start and end?

| Event | Timestamp (UTC) |
|-------|----------------|
| First suspicious activity | |
| Peak activity | |
| Last activity seen | |
| Total duration | |

**Was this outside business hours?** Yes / No
**Why does timing matter here?**

---

## 📍 WHERE
> Which device, IP address, or website was involved?

**Source (attacker side):**
- IP address:
- Hostname:
- Country/Location:
- AbuseIPDB score: /100
- VirusTotal result:

**Destination (victim side):**
- Device name:
- Internal IP:
- Operating system:
- Location (office / remote / cloud):

**URLs or domains involved:**
- URL:
- VirusTotal result:

---

## 🎯 WHY — VERDICT
> This is the most important section. Your analysis and final decision.

### Is this a true or false positive?
- [ ] ✅ TRUE POSITIVE — real threat, action needed
- [ ] ❌ FALSE POSITIVE — benign activity, close alert
- [ ] ⚠️ NEEDS MORE INVESTIGATION — escalate

### My reasoning:
> Explain WHY you made that decision. Use evidence from above.

1.
2.
3.

### Threat intelligence checked:
- [ ] VirusTotal — result:
- [ ] AbuseIPDB — result:
- [ ] MITRE ATT&CK — technique matches:

### Does this match known attack behaviour?
> e.g. "Encoded PowerShell matches T1059.001 — Command and Scripting Interpreter"

### Recommended action:
- [ ] Close alert — false positive
- [ ] Monitor — watch for more activity
- [ ] Isolate device — contain threat
- [ ] Escalate to Tier 2 — high severity
- [ ] Reset credentials — account compromised
- [ ] Block IP/domain — network level

---

## 📝 Full Narrative (optional but impressive)

> Write a short paragraph summarising the whole incident as if explaining to a colleague.
> This is what you would say in a handover meeting.

*At [TIME] on [DATE], an alert fired for [ALERT NAME]. Investigation revealed that [USER] on device [DEVICE] performed [ACTION]. The activity was [normal/abnormal] because [REASON]. Cross-referencing with threat intelligence confirmed [FINDING]. The verdict is [TRUE/FALSE POSITIVE]. Recommended action: [ACTION].*

---

## 📚 What I Learned
> Add key takeaways — tools used, techniques discovered, things to remember

-
-
-

---

## 🔗 References
> Links to any threat intel, MITRE pages, or documentation used

-
-
