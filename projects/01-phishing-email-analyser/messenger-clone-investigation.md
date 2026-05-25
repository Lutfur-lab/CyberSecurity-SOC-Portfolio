# Phishing Investigation — Messenger Clone

## Alert Details
- Domain   : messenger-one-eta.vercel.app
- Date     : 25/05/2026
- Tool     : URLScan.io
- Verdict  : TRUE POSITIVE

## Investigation Steps

### Step 1 — First Impression
- Domain contains "messenger" but hosted on vercel.app
- Not an official Facebook/Meta domain
- Suspicious immediately

### Step 2 — URLScan.io Analysis
- IP: 64.29.17.131 (Amazon AWS)
- Domain age: 2 days old
- Google Safe Browsing: MALICIOUS confirmed
- Page title: "Messenger Clone" (attacker error)

### Step 3 — Screenshot Evidence
- Fake Facebook Messenger login page
- Email + password harvesting form
- Copied Messenger branding and logo

### Step 4 — Indicators
- Domains: messenger-one-eta.vercel.app
           ws-eu.pusher.com (data exfiltration)
- IPs: 64.29.17.131 / 64.29.17.67
- 30+ file hashes identified

## Attack Summary
Type    : Credential Harvesting
Target  : Facebook Messenger users
Method  : Fake login page clone
Goal    : Steal email + password

## Actions Taken
1. Block domain at firewall
2. Block IP 64.29.17.131
3. Report to Vercel for takedown
4. Warn affected users
5. Search SIEM for anyone who visited

## Tools Used
- URLScan.io
- Google Safe Browsing
- Manual visual analysis

## Key Indicators of Compromise
- Domain: messenger-one-eta.vercel.app
- IP: 64.29.17.131
- Page Title: "Messenger Clone"
