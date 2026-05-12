# SOC Lookups Cheatsheet

> When an alert fires, context is everything. Use these two lookups before making any triage decision.

---

## The Two Core Lookups

| Lookup | Question It Answers |
|---|---|
| **Identity Inventory** | Who is this person? What is their role, location, and access? |
| **Asset Inventory** | What is this machine? What data does it hold? Who should access it? |

---

## Triage Question Flow

When you receive an alert, ask these in order:

1. **Who** triggered the alert? → Check Identity Inventory
2. **What system** was involved? → Check Asset Inventory
3. **Does the action make sense** given their role and the system's purpose?
4. **Is anything out of place?** → wrong time, unusual location, unexpected access

---

## Red Flags to Watch For

- Activity outside normal working hours
- Access from an unusual country or location
- A user accessing a system they have no business reason to use
- Service accounts performing user-like actions
- High-volume file downloads or transfers

---

## Quick Example

| Alert Element | Lookup Used | Finding |
|---|---|---|
| G.Baker logged in | Identity Inventory | CFO — finance access expected |
| HQ-FINFS-02 server | Asset Inventory | Finance file server |
| Shared file with R.Lund | Identity Inventory | US Financial Adviser — finance role |
| **Verdict** | — | **Legitimate activity** |
