# Windows Firewall IP Blocking Lab

## Objective
Block a malicious IP using Windows PowerShell

## Commands Used
# Block IP
netsh advfirewall firewall add rule name="Block Test IP" 
dir=in action=block remoteip=192.0.2.1

# Verify
netsh advfirewall firewall show rule name="Block Test IP"

# Remove
netsh advfirewall firewall delete rule name="Block Test IP"

## Real World Context
Used when malicious IP is identified from threat intel 
reports or SIEM alerts — block at perimeter firewall level
