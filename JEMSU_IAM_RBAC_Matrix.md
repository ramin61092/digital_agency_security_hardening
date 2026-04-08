# Identity & Access Management (IAM)
## Role-Based Access Control (RBAC) Matrix

**Prepared For:** JEMSU Executive Leadership & IT Security
**Prepared By:** Alireza (Ramin) Delsouz
**Subject:** Google Ads Manager Account (MCC) Access Restructuring

**Objective:** To mitigate the risk of mass-account compromise by removing standing "Global Admin" privileges and implementing strict, role-based access across the Digital Advertising department.

---

> **⚠️ Advisory Notice: Organizational Structure & Best Practices**
>
> This RBAC matrix is a theoretical model designed to illustrate security best practices. Because I do not have direct visibility into JEMSU's complete internal hierarchy, department structures, or daily operational workflows, the roles listed below are generalized. This framework serves as a baseline example of how to implement the **Principle of Least Privilege (PoLP)** and **Zero Trust architecture** within a Google Ads environment. JEMSU leadership and IT personnel should adapt and map these concepts to their actual organizational roles and business requirements.

---

## Core Security Principles Implemented

The recent malvertising breach was exacerbated by an over-privileged account. To prevent recurrence, the following IAM principles are adopted:

| Principle | Description |
|---|---|
| 🔒 **Principle of Least Privilege (PoLP)** | Users are granted only the minimum level of access necessary to perform their specific job functions. |
| ⚖️ **Separation of Duties** | The individual who manages campaigns should not be the same individual who authorizes account access or billing changes. |
| 🗂️ **Compartmentalization** | Media buyers will only have access to their assigned client sub-accounts, not the global MCC. |
| 🚫 **Zero Trust Architecture** | Never trust, always verify. Access is continuously validated and lateral movement within the MCC is restricted. |

---

## The RBAC Matrix

The following matrix defines the new standardized access levels for the JEMSU Digital Advertising team within the Google Ads environment.

| Internal JEMSU Role | Google Ads Permission Level | Scope of Access | Key Restrictions |
|---|---|---|---|
| **Director of Digital Advertising** | Standard | Global (All Sub-Accounts) | Cannot add/remove users. Cannot change overarching MCC billing. Requires hardware security key. |
| **Senior Media Buyer / Account Manager** | Standard | Segmented (Assigned Clients Only) | Restricted from viewing or altering campaigns outside their specific client roster. |
| **Junior Ad-Ops / Data Analyst** | Read-Only | Segmented (Assigned Clients Only) | Cannot alter budgets, change destination URLs, or create campaigns. Can only run reports. |
| **Finance / Accounting Controller** | Billing | Global | Cannot view or edit ad campaigns. Strictly limited to invoice and payment profile management. |
| **IT Security / System Admin** | Administrative | Global (Break-Glass Only) | Does not run campaigns. Used strictly for user provisioning, security audits, and emergency containment. |

---

## Enforcement Rules & Guardrails

To ensure this matrix remains effective, the following rules must be hardcoded into JEMSU's standard operating procedures:

### Rule 1 — The "Two-Man Rule" for Admin Actions
The IT Security Admin role is the **only** account with the ability to invite new users or change access levels. Any request to elevate a user's privileges must be:
1. Submitted via a ticketing system
2. Approved by a Department Director

### Rule 2 — Mandatory FIDO2 Binding
Any user holding **"Standard"** or **"Administrative"** access must authenticate using a hardware-bound security key (e.g., YubiKey or Google Titan Key) to prevent Adversary-in-the-Middle (AiTM) session hijacking.

### Rule 3 — Quarterly Access Audits
IT Security will conduct an access audit every **90 days** to:
- Revoke access for offboarded employees
- Revoke or adjust access for employees who have changed roles

---

## Access Level Summary

```
GLOBAL MCC
├── IT Security / System Admin  [Administrative — Break-Glass Only]
├── Finance / Accounting        [Billing — No Campaign Access]
└── Director of Digital Ads     [Standard — No User Management]

SEGMENTED (Client Sub-Accounts)
├── Senior Media Buyer          [Standard — Assigned Clients Only]
└── Junior Ad-Ops / Analyst     [Read-Only — Assigned Clients Only]
```

---

*Created by: Ramin Delsouz | Date: January 2026 | Status: Post-Incident Remediation*
