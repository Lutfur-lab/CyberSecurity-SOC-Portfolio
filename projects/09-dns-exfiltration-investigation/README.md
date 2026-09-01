# DNS Exfiltration Investigation

Traced a phishing email through to a confirmed data exfiltration incident 
using Sysmon/Splunk. Attachment was a disguised .lnk file that triggered a 
PowerShell reverse shell (ngrok), leading to financial data theft via 
DNS tunneling.

See [case-study.md](./case-study.md) for full write-up.
