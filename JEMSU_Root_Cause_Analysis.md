# Root Cause Analysis: JEMSU Ad Spend Breach

**Prepared By:** Alireza (Ramin) Delsouz
**Date Completed:** January 9, 2026
**Subject:** Unauthorized Access and Malvertising Deployment via Google Ads MCC

---

## Overview & Important Context

This Root Cause Analysis (RCA) breaks down exactly how the November 2025 breach in the Digital Advertising company JEMSU unfolded.

> **⚠️ Scope Disclosure:** This analysis is based entirely on the external sequence of events, information provided by the team, and the final outcome observed in the Google Ads environment. Direct access to JEMSU's internal network, email servers, or infrastructure logs was not available. We are analyzing the footprint the attackers left behind rather than internal system telemetry.

---

## What Happened: Timeline of the Breach

```
[1] THE LURE       → Spear-phishing email sent to Director of Digital Advertising
                     Disguised as urgent alert from Google or a major client

[2] THE TRAP       → Victim clicks link → routed through attacker proxy server
                     Victim enters credentials + approves MFA prompt (believing it's real)

[3] THE EXPLOIT    → Attacker intercepts live session cookie (not the password)
                     Attacker now holds authenticated "VIP pass" into the MCC

[4] THE DAMAGE     → Automated scripts deploy malvertising across 200 client accounts
                     ~$100,000+ in unauthorized ad spend within hours
                     Google automated systems flag anomaly and shut down activity
```

---

## The Attack Vector: Why Standard MFA Failed

A common misconception is that any form of MFA (text message code, authenticator app prompt) makes an account bulletproof against phishing. **This is no longer true.**

In an **Adversary-in-the-Middle (AiTM)** attack:

1. The attacker stands up a proxy server between the victim and the real website
2. The victim logs in and approves MFA — believing they are authenticating to the real site
3. The real website issues a **session token** (a digital pass that keeps the user logged in)
4. The attacker's proxy **intercepts that token**
5. From this point forward, the attacker no longer needs the victim's password or phone — the stolen session token grants direct, authenticated access

> The victim did nothing "wrong" in the traditional sense. They completed MFA. The vulnerability was in the **type** of MFA used — not in human error.

---

## Impact Breakdown

Because the attackers held top-level administrative access, they bypassed individual account limits and spread spend rapidly across the entire portfolio.

| Client Tier | Accounts Hit | Est. Spend per Account | Total Segment Spend |
|---|---|---|---|
| Enterprise | ~15 | $2,500 | >$37,500 |
| Mid-Market | 50 | $750 | $37,500 |
| Small Business | 135 | $185 | $25,000 |
| **Total** | **~200** | **—** | **>$100,000** |

> **Attack Pattern Noted:** The attackers deliberately targeted high-budget Enterprise accounts for maximum immediate drain, while using the volume of Small Business accounts to accumulate spend without tripping individual low-budget alarms.

---

## The Root Cause

The core issue was not simply that a phishing email bypassed spam filters, or that a link was clicked.

> **True Root Cause: An Identity and Access Management (IAM) Vulnerability.**

A single account with **"Global Admin"** privileges over 200 clients was:
- Secured with a **phishable form of MFA** (authenticator app)
- **Lacking secondary approval guardrails** for account-wide budget changes

When that single point of failure was compromised, the attackers inherited unrestricted, unmonitored power over the entire client portfolio.

### 5 Whys Analysis

| # | Why? | Answer |
|---|---|---|
| 1 | Why did $100K+ drain from 200 accounts? | An attacker had unchecked Global Admin access |
| 2 | Why did the attacker have Global Admin access? | A session cookie was stolen via AiTM attack |
| 3 | Why was the session cookie stealable? | Phishable MFA (authenticator app) was in use |
| 4 | Why was phishable MFA accepted for Global Admin? | No policy enforcing phishing-resistant MFA existed |
| 5 | Why was there no secondary check on mass budget changes? | No least-privilege or approval guardrail policy was in place |

---

## Action Plan

> We can't rely on humans to be perfect 100% of the time. We need to build a system that **fails safely.**

### 1. 🔑 Upgrade to Phishing-Resistant MFA — *Immediate*
Move all MCC admin accounts off standard authenticator apps to **hardware security keys** (YubiKey or Google Titan Security Key). Hardware keys are cryptographically bound to the physical device and the specific website domain, making them **immune to AiTM session-stealing**.

### 2. 🔒 Enforce Least Privilege — *Short-Term*
Audit the MCC. No single account should have the ability to alter budgets across 200 clients without a secondary approval ("digital handshake") from another admin. Conduct internal access audits **once per quarter**.

### 3. 📊 Implement Automated Spend Alerts — *Short-Term*
Deploy automated monitoring that triggers an **immediate account pause and team alert** if MCC-wide spend spikes abnormally within a defined time window.

### 4. 🎓 Targeted Team Training — *Ongoing*
Roll out awareness training focused on identifying high-level, admin-targeted spear-phishing lures — giving the team the tools to recognize threats when technical filters miss them.

---

## Closing Summary

This breach proves that even diligent team members can fall victim to advanced phishing. However, the root cause was not just a clicked link — it was a system architecture that allowed a single compromised account to drain over $100,000 across 200+ clients without any secondary checks.

**Three non-negotiable remediation pillars going forward:**

| Priority | Action | Impact |
|---|---|---|
| 🔴 Immediate | Mandate FIDO2 hardware keys for all admin accounts | Blocks AiTM session hijacking at the source |
| 🟡 Short-Term | Enforce least-privilege and approval workflows | Eliminates single points of catastrophic failure |
| 🟢 Ongoing | Automated spend anomaly alerts + team training | Provides real-time detection and human resilience |

---

*Created by: Ramin Delsouz | Date: January 9, 2026 | Status: Post-Incident Remediation*
