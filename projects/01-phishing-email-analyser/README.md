# 🎣 Project 01 — Phishing Email Analyser (Python)

> 🔲 **Status: Planned** — not built yet.

## Goal
A Python tool that takes a raw `.eml` file, extracts headers, URLs and sender info, then checks them against VirusTotal and AbuseIPDB to give a threat score.

## Planned features
- [ ] Parse raw `.eml` files
- [ ] Extract headers (From, Reply-To, Return-Path, Received, SPF/DKIM/DMARC results)
- [ ] Pull all URLs and attachments (with SHA256 hashes)
- [ ] Check sender IP against AbuseIPDB
- [ ] Check URLs and hashes against VirusTotal
- [ ] Score: Low / Medium / High
- [ ] Output an investigation report

## Planned stack
Python 3 · `email`, `re`, `hashlib`, `requests` · VirusTotal API · AbuseIPDB API

*Related real investigation: [Project 10 — Fake Messenger login](../10-messenger-phishing-investigation/)*
