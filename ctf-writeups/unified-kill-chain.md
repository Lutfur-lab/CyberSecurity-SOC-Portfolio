# 🔗 Unified Kill Chain — SOC Analyst Notes

**Author:** *[Your Name]*
**Topic:** Attack frameworks for SOC Level 1
**Related:** [Koi Stealer Case Study](./README.md)

---

## 1. The Core Idea

The Unified Kill Chain (Paul Pols, 2017) describes an intrusion in **18 phases**, grouped into **3 stages**:

> ## **IN → THROUGH → OUT**

| Stage | Attacker's Goal | Plain English |
|-------|-----------------|---------------|
| 🔵 **IN** | Initial foothold | Break into one machine |
| 🟡 **THROUGH** | Network propagation | Spread across the network |
| 🔴 **OUT** | Action on objectives | Steal the data / cause damage |

**Analogy:** a burglar gets **IN** through a window, moves **THROUGH** the rooms finding the safe, and gets **OUT** with the jewellery.

---

## 2. Stage Breakdown

### 🔵 IN — Initial Foothold

The attacker gains control of a single machine.

| Phase | What happens |
|-------|--------------|
| Reconnaissance | Researching the target (LinkedIn, open ports, public info) |
| Weaponization | Building the malicious payload |
| Delivery | Sending it (phishing email, malicious link) |
| Social Engineering | Convincing the user to act |
| Exploitation | Code executes on the victim machine |
| Persistence | Survives reboots (registry keys, scheduled tasks),leaving backdoor |
| Defence Evasion | Avoiding AV/EDR detection |
| Command & Control | Malware connects back to the attacker |

**Result:** attacker owns **one** machine.

---

### 🟡 THROUGH — Network Propagation

The attacker expands from that first machine across the network.

| Phase | What happens |
|-------|--------------|
| Pivoting | Using the compromised host as a tunnel deeper in.moving 1 to 1 |
| Discovery | Mapping other hosts, shares, accounts |
| Privilege Escalation | Gaining admin / SYSTEM rights |
| Execution | Running tools on other systems |
| Credential Access | Dumping passwords and hashes |
| Lateral Movement | Jumping host-to-host (SMB, RDP, WMI) |

> 🔁 **Critical concept — non-linearity:** on every new machine, the attacker **repeats the IN phases** (recon → exploit → persist → evade). The chain is a **loop**, not a straight line.

**Result:** attacker owns **many** machines, often including high-value ones.

---

### 🔴 OUT — Action on Objectives

The attacker achieves what they came for.

| Phase | What happens |
|-------|--------------|
| Collection | Gathering the target data |
| Exfiltration | Sending it out of the network |
| Impact | Ransomware, deletion, disruption |
| Objectives | Goal achieved |

**Result:** the breach — the part that makes the news.

---

## 3. Unified Kill Chain vs Cyber Kill Chain

| | Cyber Kill Chain | Unified Kill Chain |
|---|---|---|
| **Phases** | 7 | 18 |
| **Shape** | Linear (1→2→3...) | **Non-linear** (loops and repeats) |
| **Internal movement** | ❌ Not covered | ✅ Full **THROUGH** stage |
| **Basis** | Lockheed Martin, 2011 | Blends Cyber Kill Chain + MITRE ATT&CK |

**Why UKC exists:** the original Cyber Kill Chain has no proper stage for what an attacker does *after* the first foothold — lateral movement, pivoting, privilege escalation. That's the gap UKC fills.

---

## 4. Applied to a Real Investigation

Mapping the [Koi Stealer case study](./README.md) to the Unified Kill Chain:

| Time (UTC) | Observed Activity | UKC Stage |
|-----------|-------------------|-----------|
| 17:32 | Suspicious `.txt` request to external IP → host `172.17.0.99` infected | 🔵 **IN** (Delivery / Exploitation) |
| 17:33 | SMBv1, NTLMSSP overflow, IPC$ share access against `172.17.0.17` | 🟡 **THROUGH** (Lateral Movement) |
| 17:34 | Kerberos principal name overflow attempt | 🟡 **THROUGH** (Credential Access) |
| 17:35 | Koi Stealer C2 check-in ×48 to `79.124.78.197` | 🔴 **OUT** (C2 / Exfiltration) |

> 💡 The Cyber Kill Chain has nowhere clean to place the 17:33 SMB activity. The Unified Kill Chain does — it's textbook **THROUGH**.

---

## 5. Key Points to Remember

- **Three stages: IN → THROUGH → OUT.**
- **IN** = foothold on one machine.
- **THROUGH** = spreading across the network (the gap the old model missed).
- **OUT** = collection, exfiltration, impact.
- **Non-linear** — the attacker repeats IN phases on every new host.
- 18 phases total, but for SOC L1 the **3 stages and the concept** are what matter.

---

## 6. Interview Questions

**Q: What's the difference between the Cyber Kill Chain and the Unified Kill Chain?**
> The UKC has 18 phases across three stages (In, Through, Out) versus the CKC's 7, it's non-linear rather than a straight line, and it covers internal network propagation — lateral movement, pivoting, privilege escalation — which the Cyber Kill Chain ignores.

**Q: Why is a non-linear attack model more realistic?**
> Because attackers don't move in one straight line. Each time they reach a new host they repeat reconnaissance, exploitation, persistence and evasion on that host. Real intrusions loop.

**Q: Where does lateral movement sit in the Unified Kill Chain?**
> In the **Through** stage — network propagation.

---

*SOC Level 1 study notes. Part of my cyber security learning portfolio.*
