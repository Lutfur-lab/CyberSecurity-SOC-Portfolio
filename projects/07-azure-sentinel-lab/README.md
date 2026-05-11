# ☁️ Project 07 — Azure Sentinel Lab (Free Tier)

## What is this?
A fully documented setup of Microsoft Sentinel on a free Azure account, with real data connectors, custom KQL detection rules, and investigation walkthroughs.

## Why employers love this
The SOC Analyst job description you found requires Microsoft Sentinel. This project proves hands-on Sentinel experience before your first job — extremely rare and highly valued.

## Setup guide

### Step 1 — Create free Azure account
- Go to azure.microsoft.com/free
- Get £150 free credit — more than enough

### Step 2 — Deploy Sentinel
- Create Log Analytics workspace
- Enable Microsoft Sentinel on the workspace
- Free tier: 10GB/day for 31 days

### Step 3 — Connect data sources (free)
- Azure Activity logs
- Azure AD Sign-in logs
- Microsoft Defender for Cloud (free tier)

### Step 4 — Write detection rules
- Go to Analytics > Create scheduled query rule
- Use KQL queries from Project 03

### Step 5 — Trigger and investigate alerts
- Simulate failed logins to Azure portal
- Watch alerts fire in Sentinel
- Document the investigation

## What to document
- [ ] Setup screenshots step by step
- [ ] Data connectors configured
- [ ] Custom detection rules (KQL)
- [ ] Sample alert investigations with screenshots
- [ ] Sentinel dashboard overview

## Skills shown
Microsoft Sentinel · Azure · KQL · Cloud SIEM · Detection engineering · Documentation
