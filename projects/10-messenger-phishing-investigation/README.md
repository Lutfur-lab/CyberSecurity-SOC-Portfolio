# 🎣 Project 10 — Phishing Investigation: Fake Messenger Login

## Alert Details
| | |
|---|---|
| URL | `messenger-one-eta.vercel.app` |
| Date | 25/05/2026 |
| Tools | URLScan.io, Google Safe Browsing |
| Verdict | ✅ **TRUE POSITIVE** — credential harvesting |

## Investigation Steps

### Step 1 — First impression
- The name contains "messenger" but it's hosted on `vercel.app`, a free hosting platform
- Not an official Meta/Facebook domain → suspicious straight away

### Step 2 — URLScan.io analysis
- Resolved IP: `64.29.17.131` (shared cloud hosting behind vercel.app)
- First seen: ~2 days before analysis (note: `vercel.app` subdomains have no WHOIS age of their own, so "first seen" is the useful signal)
- Google Safe Browsing: flagged **malicious**
- Page title: "Messenger Clone" — the attacker left the template name in place

### Step 3 — Page content
- Fake Facebook Messenger login page with copied branding and logo
- Form collecting email + password
- Page talks to `ws-eu.pusher.com` — a legitimate real-time messaging service, abused here to send captured credentials back to the attacker

## Attack Summary
| | |
|---|---|
| Type | Credential harvesting |
| Target | Facebook Messenger users |
| Method | Cloned login page on free hosting |
| Goal | Steal email + password |

## Recommended Actions
1. **Block the URL/domain** at the web proxy and DNS filter — *not* the IP, as it's shared hosting and blocking it would break legitimate sites
2. Report the site to Vercel's abuse team for takedown
3. Search proxy/DNS logs for any user who visited the URL
4. For any user who submitted credentials: force password reset and review recent sign-ins
5. Warn staff with a short awareness notice

## Indicators
| Type | Value | Action |
|---|---|---|
| URL | `messenger-one-eta.vercel.app` | Block |
| Page title | "Messenger Clone" | Hunting pivot on URLScan |
| IP | `64.29.17.131`, `64.29.17.67` | Context only — shared hosting, do not block |
| Service | `ws-eu.pusher.com` | Context only — legitimate service abused |

## What I learned
Free hosting platforms give phishing pages a trusted-looking HTTPS domain for free. The IP is useless as a block indicator on shared hosting — the URL is what matters.
