# 🎣 Project 01 — Phishing Email Analyser

## What is this?
A Python tool that analyses suspicious emails automatically. Given a raw .eml file, it extracts headers, URLs, and sender info — then cross-checks against VirusTotal and AbuseIPDB APIs to score the threat level.

## Why employers love this
Phishing is the #1 task for Tier 1 SOC analysts. This project proves you can think like an analyst, use real threat intel APIs, and automate repetitive SOC tasks — not just study theory.

## Features
- [ ] Parse raw .eml email files
- [ ] Extract email headers (From, Reply-To, X-Originating-IP)
- [ ] Pull all URLs from email body
- [ ] Check sender IP against AbuseIPDB API
- [ ] Check URLs against VirusTotal API
- [ ] Generate threat score: Low / Medium / High
- [ ] Output clean investigation report

## Tools & Technologies
- Python 3
- VirusTotal API (free tier)
- AbuseIPDB API (free tier)
- Libraries: email, re, requests, json

## Sample output
```
===== PHISHING ANALYSIS REPORT =====
Email From:    support@amaz0n-verify.com
Reply-To:      harvester99@gmail.com
Sender IP:     185.220.101.45
IP Reputation: HIGH RISK (AbuseIPDB score: 92/100)
URLs found: 3
  [MALICIOUS]  http://amaz0n-verify.com/login  VT: 14/72 flagged
  [CLEAN]      https://amazon.com
  [SUSPICIOUS] http://bit.ly/3xR9abc  VT: 2/72 flagged
VERDICT: HIGH RISK — Likely phishing
=====================================
```

## Skills shown
Python scripting · Phishing analysis · Threat Intel APIs · SOC automation
