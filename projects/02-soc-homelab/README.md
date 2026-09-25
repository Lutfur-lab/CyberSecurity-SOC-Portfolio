# 🏠 Project 02 — SOC Home Lab

> 🔲 **Status: Planned** — lab build not started yet. Completed mini-lab: [Windows Firewall IP blocking](./windows-firewall-ip-blocking.md)

## Planned architecture
```
[Kali Linux — Attacker VM]
         │ attacks
         ▼
[Windows 10 — Target VM + Sysmon]  ──logs──▶  [Wazuh or Security Onion — SIEM]
                                                        │
                                                        ▼
                                              [Analyst — investigate alerts]
```

## Planned tools
VirtualBox · Wazuh or Security Onion · Windows 10 evaluation VM · Sysmon · Kali Linux

## Planned attack scenarios
| Attack | Tool | Expected detection |
|---|---|---|
| Port scan | nmap | Network scan alerts |
| Brute force | Hydra | Failed logons (4625), then success (4624) |
| Reverse shell | Metasploit | Process creation (4688 / Sysmon 1), network connection (Sysmon 3) |
| Persistence | schtasks | Scheduled task created (4698) |

## To document when built
- [ ] Setup screenshots
- [ ] Each attack + the alert it triggered
- [ ] Investigation write-up per scenario
