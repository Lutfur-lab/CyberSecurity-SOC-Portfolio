# 📧 Email Header Analysis — SOC Analyst Notes

**Author:** *[Lutfur]*
**Topic:** Phishing investigation fundamentals (SOC Level 1)
**Priority:** 🔴 Essential — core daily task for a Tier 1 analyst

---

## 1. The Core Idea

The **email body can lie. The header is where the truth lives.**

Headers are the hidden metadata on every email — they record the true sender, every server the message passed through, and whether it passed authentication. Reading them is how you decide: **legitimate or spoofed?**

> Think of the header as the **crime scene** of a phishing email. Every phishing ticket starts here.

---

## 2. How Email Travels (the foundation)

| Step | What happens | Protocol |
|------|--------------|----------|
| You hit send | Client pushes mail to your mail server | **SMTP** |
| Server looks up recipient | "Where does this domain receive mail?" | **DNS → MX record** |
| Message delivered | Travels across the internet to their server | **SMTP** |
| Recipient opens inbox | Client pulls the message down | **POP3 / IMAP** |

- **SMTP** = sends mail out
- **DNS / MX** = finds the recipient's mail server
- **POP3** = downloads to one device (old-school)
- **IMAP** = syncs across all devices (modern standard)

Header analysis = tracing this journey backwards to find where a message *really* came from.

---

## 3. Key Header Fields

| Field | What it is | Red flag if... |
|-------|-----------|----------------|
| `From:` | What the user sees | Easily spoofed — **never trust alone** |
| `Return-Path:` | Envelope sender (where bounces go) | Doesn't match `From:` |
| `Reply-To:` | Where replies actually go | Different domain than `From:` |
| `Received:` | The server hop chain | Origin IP from unexpected host/country |
| `Message-ID:` | Unique message identifier | Domain doesn't match sender |
| `Authentication-Results:` | SPF / DKIM / DMARC verdicts | Any `fail` |

**Golden rule:** Read the `Received:` chain **bottom-to-top**. The oldest hop (the true origin) is at the *bottom*; each server adds its line on *top* as the mail passes through.

---

## 4. The Three Authentication Checks

Found in the `Authentication-Results:` header. **All three should say `pass`.**

| Check | Question it answers | Simple meaning |
|-------|--------------------|----------------|
| **SPF** | Is the sending server allowed to send for this domain? | Checks the sender's *address* |
| **DKIM** | Was the message tampered with in transit? | Checks the *signature/integrity* |
| **DMARC** | What to do if SPF/DKIM fail? | The *policy* (none / quarantine / reject) |

**Memory hook:**
- **SPF** = is the sender **P**ermitted? (Sender Permitted From)
- **DKIM** = was the message **K**ept intact? (signature)
- **DMARC** = the **decision** when the others fail

---

## 5. The Red-Flag Checklist

When triaging, hunt for these:

1. ❌ SPF / DKIM / DMARC = **fail** or **none**
2. ❌ `From:` doesn't match `Return-Path:`
3. ❌ `Reply-To:` points to a different domain
4. ❌ Originating IP (bottom `Received:`) from an unexpected host/country
5. ❌ `Message-ID` domain doesn't match the sender domain
6. ❌ **Lookalike domain** — `paypa1.com` (number 1), `micros0ft.com` (zero)
7. ❌ Body pressure tactics — urgency, threats, "verify now"

Any one of these pushes the verdict toward **malicious**.

---

## 6. Worked Example (spoofed PayPal)

```
Received: from unknown-host (185.220.101.47) by mail.company.com ...
Authentication-Results: mx.google.com;
        spf=fail (sender IP is 185.220.101.47) smtp.mailfrom=security@paypa1-alerts.com;
        dkim=none;
        dmarc=fail (p=REJECT) header.from=paypal.com
From: "PayPal Security" <service@paypal.com>
Return-Path: <security@paypa1-alerts.com>
Reply-To: <recover-account@mailbox-verify.ru>
Message-ID: <8842xk@paypa1-alerts.com>
Subject: Urgent: Your account has been limited - verify now
```

**Findings:**
- SPF **fail**, DKIM **none**, DMARC **fail (reject)** — all three failed.
- `From:` = paypal.com but `Return-Path:` = **paypa1**-alerts.com (number 1 = lookalike).
- `Reply-To:` = a `.ru` domain — replies go to the attacker.
- `Message-ID` domain = paypa1-alerts.com — confirms true origin.
- Originating IP `185.220.101.47` — enrich on AbuseIPDB (Tor/abuse ranges).

**Verdict:** 🔴 Malicious — spoofed PayPal phishing.
**Action:** block `paypa1-alerts.com` + IP `185.220.101.47`, purge from inboxes, warn users.

---

## 7. Investigation Workflow (every time)

1. Pull the **raw headers**.
2. Read `Received:` **bottom-to-top** → find the true origin IP.
3. Check **SPF / DKIM / DMARC** in `Authentication-Results:`.
4. Compare **`From:` vs `Return-Path:` vs `Reply-To:`** for mismatches.
5. Check the **originating IP** on AbuseIPDB / VirusTotal.
6. Extract & **defang** IOCs (`hxxp://`, `evil[.]com`).
7. **Verdict → action → ticket.**

---

## 8. Tools

- **MXToolbox Email Header Analyzer** — paste raw headers, get parsed hops + auth results.
- **Google Admin Toolbox Messageheader** — same idea, Google's version.
- **AbuseIPDB / VirusTotal** — reputation-check the originating IP.

---

## 9. Interview Questions

**Q: How do you find where an email really came from?**
> Read the `Received:` chain bottom-to-top — the lowest hop shows the true originating server and IP.

**Q: What are SPF, DKIM, and DMARC?**
> SPF checks whether the sending server is authorised for the domain; DKIM verifies the message wasn't altered in transit via a signature; DMARC is the policy that decides what happens when SPF or DKIM fail.

**Q: You receive a phishing report — which header fields do you check and why?**
> `From` vs `Return-Path` vs `Reply-To` for mismatches, `Authentication-Results` for SPF/DKIM/DMARC verdicts, and the `Received` chain for the true origin IP — then I enrich that IP against threat intel.

---

## 10. Remember This

- Body lies, **headers tell the truth**.
- Read `Received:` **bottom-to-top**.
- `From:` is **easily faked** — always cross-check `Return-Path:` and `Reply-To:`.
- **SPF/DKIM/DMARC should all pass** — any fail = investigate.
- Watch for **lookalike domains** and **urgency** tactics.
- Always finish with **verdict + action + ticket**.

---

*SOC Level 1 study notes. Part of my cyber security learning portfolio.*
