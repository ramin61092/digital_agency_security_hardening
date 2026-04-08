# JEMSU Hardware Key (FIDO2) Implementation Guide
## Enforcing Phishing-Resistant MFA for Google Ads MCC Access

**Prepared For:** JEMSU IT & Security Operations
**Prepared By:** Alireza (Ramin) Delsouz
**Subject:** FIDO2 Security Key Rollout for Google Ads MCC Access
**Objective:** To completely deprecate phishable authentication methods (SMS, Voice, Authenticator Apps) for highly privileged accounts and enforce hardware-bound security keys.

---

> **⚠️ Advisory Notice**
>
> This implementation guide outlines best practices for enforcing phishing-resistant MFA within a Google Workspace environment. It is an advisory document designed to prevent credential harvesting and Adversary-in-the-Middle (AiTM) session hijacking. JEMSU IT administrators should **test these configurations in a sandbox Organizational Unit (OU) before deploying globally** to prevent accidental lockouts.

---

## Background & Why This Matters

The November 2025 JEMSU breach succeeded because the compromised account was protected by a **phishable form of MFA** (an authenticator app). In an AiTM attack, the attacker's proxy intercepts the session token in real time — meaning even a correctly approved MFA prompt provides zero protection.

**FIDO2 hardware security keys solve this at the hardware level.** The key is cryptographically bound to both the physical device and the specific website domain. A proxy server cannot intercept or replay the authentication — even if the user is tricked into visiting a fake site, the key will simply refuse to authenticate.

---

## Step 1: Procurement & Distribution

JEMSU must procure FIDO2/WebAuthn compliant hardware keys for all privileged MCC accounts.

| Recommendation | Detail |
|---|---|
| 🔑 **Primary Hardware** | YubiKey 5 NFC or YubiKey 5C NFC (depending on endpoint USB port type) |
| 🔁 **Redundancy Requirement** | Every user **must be issued two keys** — one as daily primary (kept on keychain), one registered and stored securely (home safe or office lockbox) as backup |
| 👥 **Who Needs a Key** | Director of Digital Advertising, IT Security Admin, any account with Standard or Administrative MCC access (per the [RBAC Matrix](./JEMSU_IAM_RBAC_Matrix.md)) |

---

## Step 2: User Registration (Self-Service)

Before IT can enforce hardware key authentication, privileged users must register their physical devices to their JEMSU Google Workspace accounts.

**Instructions for the User:**

1. Navigate to your Google Account: `myaccount.google.com`
2. Select **Security** from the left-hand navigation panel
3. Under *"How you sign in to Google"*, select **2-Step Verification**
4. Click **Security Key** → **Add Security Key**
5. Insert your YubiKey into the USB port and **tap the gold sensor** when prompted by the browser
6. Name the key clearly (e.g., `Primary YubiKey 5C - Ramin`) and repeat the full process for your backup key

> ✅ **Completion Check:** The user should now see two registered security keys listed under their 2-Step Verification settings before proceeding to Phase 2.

---

## Step 3: Administrator Enforcement (Zero Trust Policy)

Once all targeted users have registered their keys, IT must configure Google Workspace to **reject all other forms of MFA** for these specific roles.

> ⚠️ **Critical Note:** If SMS or Authenticator app prompts remain enabled as "fallback" methods, an attacker can trigger the fallback during an AiTM attack — rendering the hardware key useless. Fallback methods must be fully disabled.

**Instructions for the IT Administrator:**

1. Log into the Google Workspace Admin Console: `admin.google.com`
2. Navigate to **Security** → **Authentication** → **2-Step Verification**
3. In the left organizational tree, select the specific **Organizational Unit (OU)** housing Digital Advertising Directors and MCC Admins
   > ⚠️ Do **not** apply this to the root OU immediately — you may lock out the entire organization
4. Under *"2-Step Verification"* policy, check **Allow users to turn on 2-Step Verification**
5. Under *"Enforcement"*, set the policy to **On**
6. Under *"Allowed 2-Step Verification methods"*, change the dropdown from `Any` to **Only Security Key**
7. Click **Save**

---

## Step 4: Break-Glass Emergency Account Configuration

If the primary IT Security Admin loses both hardware keys, the organization could be permanently locked out of the Google Workspace tenant. A **Break-Glass Emergency Access Account** prevents this scenario.

| Configuration Item | Requirement |
|---|---|
| 📧 **Account** | Dedicated global admin account (e.g., `emergency.admin@jemsu.com`) |
| 🔐 **Passphrase** | Exceptionally long, randomly generated — never reused elsewhere |
| 🔑 **Key** | Dedicated FIDO2 key registered exclusively to this account |
| 🏦 **Physical Storage** | Passphrase + YubiKey stored in a tamper-evident safe at JEMSU headquarters |
| 🚨 **Alerting** | Any login attempt on this account triggers an **immediate high-priority alert** to all executives |

> This account should never be used for day-to-day operations. Its sole purpose is emergency recovery.

---

## Implementation Checklist

| Task | Owner | Status |
|---|---|---|
| Procure YubiKey 5 NFC / 5C NFC (x2 per user) | IT Security | ☐ |
| Users register primary key to Google Account | Each User | ☐ |
| Users register backup key to Google Account | Each User | ☐ |
| Backup keys stored in secure location | Each User + IT | ☐ |
| Google Workspace OU policy set to "Only Security Key" | IT Admin | ☐ |
| Break-Glass account created and secured | IT Admin | ☐ |
| Break-Glass alert rule configured | IT Admin | ☐ |
| Quarterly access audit scheduled | IT Security | ☐ |

---

## Related Documents

- [Root Cause Analysis — JEMSU Ad Spend Breach](./JEMSU_Root_Cause_Analysis.md)
- [Incident Response Playbook](./JEMSU_Incident_Response_Playbook.md)
- [IAM & RBAC Matrix](./JEMSU_IAM_RBAC_Matrix.md)

---

*Created by: Ramin Delsouz | Date: January 2026 | Status: Post-Incident Remediation*
