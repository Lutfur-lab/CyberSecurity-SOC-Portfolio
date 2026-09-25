# 🧱 Windows Firewall — Blocking a Malicious IP

## Objective
Block an IP identified as malicious on a Windows host, verify the rule, then remove it.

## Using `netsh` (Command Prompt, run as Administrator)
```cmd
:: Block inbound traffic from the IP
netsh advfirewall firewall add rule name="Block Test IP" dir=in action=block remoteip=192.0.2.1

:: Verify
netsh advfirewall firewall show rule name="Block Test IP"

:: Remove
netsh advfirewall firewall delete rule name="Block Test IP"
```

## Using PowerShell (run as Administrator)
```powershell
# Block inbound and outbound
New-NetFirewallRule -DisplayName "Block Test IP" -Direction Inbound  -RemoteAddress 192.0.2.1 -Action Block
New-NetFirewallRule -DisplayName "Block Test IP" -Direction Outbound -RemoteAddress 192.0.2.1 -Action Block

# Verify
Get-NetFirewallRule -DisplayName "Block Test IP"

# Remove
Remove-NetFirewallRule -DisplayName "Block Test IP"
```

> `192.0.2.1` is a reserved documentation IP — safe for testing.

## Real-world context
- This is a **host-based** block — useful for containing a single machine during an incident.
- Organisation-wide blocks happen at the **perimeter firewall, web proxy or EDR**, not on each host.
- Outbound blocks matter most for C2: stopping an infected host calling out.
- Never block a shared hosting / CDN IP — block the domain or URL instead.
