# ☁️ Project 07 — Microsoft Sentinel Lab

> 🔲 **Status: Planned** — not built yet.

## Goal
Deploy Microsoft Sentinel on a free Azure account, connect real log sources, write custom detection rules, and investigate the alerts they raise.

## Plan

### 1. Azure account
- Free Azure account (includes starter credit — check current amount on the Azure site)
- Set a **budget alert** first so nothing runs up a bill

### 2. Deploy Sentinel
- Create a Log Analytics workspace
- Enable Microsoft Sentinel on it (free trial period for new workspaces — check current terms)

### 3. Connect data sources
| Source | Works on free account? | Notes |
|---|---|---|
| Azure Activity logs | ✅ | Subscription-level events |
| Windows VM Security Events (via Azure Monitor Agent) | ✅ | Best source for 4625/4688 detections — needs a small VM |
| Microsoft Defender for Cloud (free tier) | ✅ | Basic recommendations/alerts |
| Entra ID (Azure AD) **sign-in logs** | ⚠️ | Exporting sign-in logs needs an **Entra ID P1/P2 licence** — use a P2 trial or skip |

### 4. Detection rules
- Analytics → Create → Scheduled query rule
- Use queries from [Project 03](../03-kql-spl-query-library/)

### 5. Trigger and investigate
- Generate failed logons against the Windows VM (RDP only from your own IP)
- Confirm the alert fires, then investigate the incident in Sentinel
- **Delete the VM afterwards** — an exposed VM is a real risk

## To document when built
- [ ] Setup screenshots
- [ ] Connectors configured
- [ ] Custom rules + the alerts they raised
- [ ] One full incident investigation write-up
