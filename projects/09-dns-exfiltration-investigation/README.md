# 🧬 Project 09 — DNS Exfiltration Investigation

**Environment:** TryHackMe SOC Simulator · **Tools:** Splunk, Sysmon, CyberChef, PowerShell

Traced a low-severity phishing alert through to a confirmed data breach. The attachment was a `.pdf.lnk` shortcut disguised as a PDF, which launched an in-memory PowerShell reverse shell over ngrok. The attacker then mapped a financial records share, staged the data and exfiltrated it via DNS tunnelling.

| | |
|---|---|
| Result | Confirmed compromise — single host, financial data exfiltrated |
| Delivery → C2 | 14 seconds |
| Key pivot | `process.parent.pid` in Splunk to rebuild the full process chain |
| Scope check | Only `win-3450` contacted the exfil domain |

➡️ **[Read the full case study](./case-study.md)**
