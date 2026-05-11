# 🏠 Project 02 — SOC Home Lab Setup

## What is this?
A fully documented home lab simulating a real SOC environment using free tools. Built with VirtualBox, Security Onion as the SIEM, a Windows VM as target, and Kali Linux as attacker.

## Why employers love this
This proves you did not just watch videos — you built a real environment, generated real attacks, and detected them. Almost no entry-level candidate does this.

## Lab Architecture
```
[Kali Linux — Attacker VM]
         |
         | attacks
         v
[Windows 10 — Target VM]  -->  [Security Onion / Wazuh — SIEM]
                                         |
                                         v
                               [You — investigating alerts]
```

## Tools (all free)
- VirtualBox — virtualbox.org
- Security Onion or Wazuh — free SIEM
- Windows 10 evaluation VM
- Kali Linux
- Sysmon on Windows VM

## Attack scenarios to simulate
| Attack | Tool | What to detect |
|--------|------|----------------|
| Port scan | nmap | Network scan alerts |
| Brute force | Hydra | Failed login events (4625) |
| Reverse shell | Metasploit | Suspicious process (4688) |
| Persistence | Schtasks | Scheduled task (4698) |

## Skills shown
SIEM setup · Network monitoring · Threat detection · Virtualisation · Documentation
