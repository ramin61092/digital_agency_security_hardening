# 🚨 JEMSU "Fire Drill" Checklist
### Immediate Response: Suspected Account Compromise

> **Print this out and keep it accessible for the Ad-Ops team.**
> If you suspect an account compromise — **DO NOT WAIT.** Execute the following steps immediately, in order.

---

## ⚡ Emergency Response Steps

### ☐ Step 1 — Sound the Alarm
Notify the **Director of Digital Advertising** and the **IT/Security Lead** immediately via **Slack or phone**.

> ⚠️ Do **NOT** use email to communicate during an active incident — the attacker may have access to the compromised user's inbox and could be monitoring communications in real time.

---

### ☐ Step 2 — Stop the Spend
Log into the **Google Ads MCC** and immediately:
- **PAUSE** all affected sub-accounts, OR
- Set all account daily budgets to **$0.00**

> This cuts off the attacker's ability to drain client funds while the investigation is underway.

---

### ☐ Step 3 — Terminate Active Sessions
The compromised user must:
1. Go to `myaccount.google.com`
2. Navigate to **Security** → **Manage all devices**
3. Select **Sign out of all sessions**

> Changing a password alone will NOT kick out an attacker who stole a session cookie via AiTM. You must invalidate the session directly.

---

### ☐ Step 4 — Revoke Unauthorized Access
In the **Google Ads MCC**:
1. Navigate to the **Access and Security** tab
2. Review every user listed
3. **Immediately delete any user you do not explicitly recognize**

---

### ☐ Step 5 — Reset Passwords
The compromised user changes their **Google Workspace password** immediately.

> Once sessions are terminated (Step 3) and unauthorized users are removed (Step 4), a full password reset closes the door on the attacker's credentials.

---

### ☐ Step 6 — Document the Damage
In the **Google Ads MCC**:
1. Navigate to **Change History**
2. Filter by the compromised user's email
3. Set the date range to the **last 24 hours**
4. **Export the full log** — this becomes your evidence record for remediation and any Google fraud claims

---

### ☐ Step 7 — Preserve the Phishing Email
If a phishing email initiated this incident:
- **DO NOT delete it**
- Forward it to IT immediately
- IT needs the **full email headers** to determine how it bypassed spam filters and to identify the attack infrastructure

---

## ✅ Checklist Summary

| # | Action | Owner | Done? |
|---|---|---|---|
| 1 | Notify Director + IT/Security via Slack or phone | First Responder | ☐ |
| 2 | Pause all affected accounts or set budgets to $0 | Ad-Ops / Director | ☐ |
| 3 | Sign out of all active Google sessions | Compromised User | ☐ |
| 4 | Revoke unrecognized users from MCC Access & Security tab | IT / Director | ☐ |
| 5 | Reset Google Workspace password | Compromised User | ☐ |
| 6 | Export Change History log for last 24 hours | IT / Ad-Ops | ☐ |
| 7 | Preserve phishing email — do not delete | Compromised User | ☐ |

---

## 📋 After Immediate Containment

Once all 7 steps above are complete, escalate to the full incident response process:

➡️ See the **[JEMSU Incident Response Playbook](./JEMSU_Incident_Response_Playbook.md)** for detailed eradication, recovery, and post-incident procedures.

---

*Created by: Ramin Delsouz | Date: January 2026 | Status: Post-Incident Remediation*
