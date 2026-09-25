# Handling Malicious Attachments & Links — my notes

Notes I made while learning how to deal with dodgy files and links in phishing emails. Writing it how I'd actually explain it to myself.

## The rule I can't forget

Don't open it. Don't click it. Don't run it. Ever.

Everything you do, you do *around* the file — hashes, sandboxes, scanners. The second you double-click that PDF on your own machine, you've potentially infected yourself. So the whole game is figuring out what something is *without* actually touching it.

The way I think about it: for anything I get, I do the same 3 things.
1. Work out what it actually is (real file type, real domain).
2. Scan it or blow it up somewhere safe (VirusTotal, or a sandbox / URLScan).
3. Grab the IOCs, defang them, write it up.

Files → hash it and sandbox it. Links → URLScan it. Simple.

---

## PDFs

PDFs are sneaky because people trust them. But they can hide JavaScript, auto-run actions, or just be a lure with a link to a fake login page inside.

What I do:
- Hash it first, without opening. On my Windows box:
  `Get-FileHash -Algorithm SHA256 "suspicious.pdf"`
- Drop that hash into VirusTotal. If loads of vendors flag it, I'm basically done — I never had to open it.
- If VirusTotal's never seen it, I throw it in a sandbox (Any.Run is the fun one, you can watch it live — Hybrid Analysis and Joe Sandbox also work). It opens the file in a throwaway VM and tells me what it tries to do.
- If I've got my lab up, pdfid / pdf-parser will flag scary keywords like /JavaScript, /OpenAction, /Launch. A PDF that wants to launch something is not a normal PDF.

Bad signs: VirusTotal hits, JavaScript baked in, or the sandbox shows it phoning out to some sketchy domain.

---

## Images

Honestly, a normal image that just shows a picture usually can't do much on its own. The trick is that it's often *not actually an image*. Stuff to watch for:
- A fake image that's really an exe — like `invoice.jpg.exe`. The double extension is the giveaway.
- Something hidden inside it (steganography).
- A "picture" that's really just bait for a link.

What I do:
- Check what it *actually* is, don't trust the name:
  `file suspicious.jpg`
  If `file` comes back saying it's an executable, that's my red flag right there.
- Eyeball the filename for double extensions.
- Hash it → VirusTotal like always.
- `exiftool suspicious.jpg` to peek at the metadata if I'm being thorough.

If it turns out to be a genuine image and nothing's flagged, it's probably fine — but the *email* around it might still be phishing, so I don't drop my guard.

---

## Videos

Basically the same story as images. The video itself is rarely the weapon. It's usually:
- A fake video that's actually an exe (`movie.mp4.exe` again).
- A "click here to watch" that's really just a link to a bad site.

What I do:
- Check the real file type with `file`.
- Look for double extensions.
- Hash → VirusTotal.
- If it's really a "click to watch" link, I stop treating it as a file and treat it as a URL (below).

---

## Links — this is the big one

This is what I'll see most. Golden rule again: don't click.

What I do:
- Defang it first so nobody clicks it by accident. `https://evil.com` becomes `hxxps://evil[.]com`.
- Then I let a tool visit it for me:
  - URLScan.io is my main one — it visits the site in a sandbox and shows me screenshots, what domains it talked to, and where it redirects. Love this tool.
  - VirusTotal (URL tab) for a reputation check.
  - AbuseIPDB for the hosting IP.
- Then I actually *look* at the URL for the classic tricks:
  - Lookalike domains — paypa1.com (that's a number 1), micros0ft-login.com.
  - Subdomain games — paypal.com.evil.ru. The real domain is evil.ru, the paypal bit is just a subdomain to fool you.
  - Shortened links (bit.ly) hiding where they really go — I expand them, never click.
  - The @ trick — https://trusted.com@evil.com actually goes to evil.com.
- Follow the redirects to see where it really lands. URLScan shows the whole chain.
- Pull out the IOCs: the full URL, the final domain, the IP.

Bad signs: URLScan or VirusTotal flags it, it lands on a fake login page, lookalike domain, or it bounces you through a redirect to somewhere nasty.

---

## My tools (the ones I keep reaching for)

- Hash a file → `Get-FileHash` (PowerShell) or `sha256sum` on Linux
- Reputation check → VirusTotal
- Blow up a file safely → Any.Run, Hybrid Analysis, Joe Sandbox
- Check a link safely → URLScan.io
- What is this file really → `file`
- Image metadata → exiftool
- IP reputation → AbuseIPDB

---

## How I write it up

I keep the report simple and always the same shape so I don't forget anything:

```
Date/time:
Severity:
Reported by:

Email: sender, From vs Return-Path vs Reply-To, auth results

The bad thing:  [PDF / image / video / URL]
  - name or URL (defanged): invoice[.]pdf  /  hxxps://evil[.]com
  - SHA256 hash:
  - what it actually is (from 'file'):

What I found:
  - VirusTotal: X/70 flagged
  - Sandbox: what it did (called out to C2, dropped an exe, etc.)
  - URLScan: phishing page / redirect chain

IOCs:
  - defanged URL
  - IP
  - hash

Verdict: true positive / false positive
Action: block the sender + domain + IP, purge it from inboxes,
        warn users, escalate to L2 if someone already clicked
```

---

## Stuff to actually remember

- Never open / click / run the real thing. This is the whole job in one line.
- Files → hash them, VirusTotal, sandbox anything unknown.
- Images and videos → check what they *really* are, watch for double extensions.
- Links → URLScan, never click, watch for lookalike domains and redirects.
- Always defang: hxxps:// and evil[.]com.
- Every investigation ends the same way: verdict, action, ticket.

---

## Interview answers I want ready

**"You get a suspicious PDF — what do you do?"**
I hash it without opening it, check the hash on VirusTotal, and if it's unknown I detonate it in a sandbox like Any.Run to see how it behaves. I never open it on my own machine. Then I pull the IOCs and report it.

**"How do you safely check a suspicious link?"**
Defang it, then use URLScan.io to visit it in a sandbox and VirusTotal for reputation — I never click it myself. I look for lookalike domains, redirect chains, and whether it lands on a fake login page.

**"What's wrong with a file called invoice.pdf.exe?"**
Double extension trick. It's actually an exe pretending to be a PDF — the real extension is .exe. Opening it runs the malware.
