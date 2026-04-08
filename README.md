# 🔐 JEMSU Digital Agency — Security Hardening Engagement
### Incident Response & IAM Hardening Following an AiTM Compromise

**Prepared By:** Alireza (Ramin) Delsouz | [LinkedIn](https://www.linkedin.com/in/alireza-delsouz)
**Date:** January 2026
**Status:** ✅ Post-Incident Remediation & Policy Generation Complete

---

> **⚠️ Advisory Disclaimer**
>
> This repository contains independent consulting documentation, methodologies, and recommended best practices for mitigating an account compromise and malvertising event. It is **not** an official JEMSU document and does not necessarily reflect JEMSU's internal policies, existing security posture, or standard operating procedures. All structures, including the RBAC matrix, are theoretical models designed to illustrate Zero Trust principles based on external findings.

---

## 📋 Executive Summary

This repository documents the full incident response, root cause analysis, and security hardening strategy following a major breach within the **JEMSU Digital Advertising** division.

A sophisticated **Adversary-in-the-Middle (AiTM)** spear-phishing campaign targeted the Director of Digital Advertising, bypassing standard Multi-Factor Authentication (MFA) to steal an active session token. The threat actors leveraged this compromised **"Global Admin"** access within the Google Ads Manager Account (MCC) to deploy malvertising payloads across **200 client accounts**, resulting in over **$100,000 USD** in unauthorized ad spend before containment.

| Detail | Value |
|---|---|
| 🎯 Attack Type | Adversary-in-the-Middle (AiTM) Spear Phishing |
| 🔓 Access Gained | Google Ads MCC — Global Admin |
| 📢 Accounts Affected | ~200 Client Sub-Accounts |
| 💸 Financial Impact | >$100,000 USD in unauthorized ad spend |
| 🛡️ Root Cause | Over-privileged account secured with phishable MFA |

---

## 🔑 Key Findings & Core Recommendations

| Finding | Recommendation |
|---|---|
| Global Admin account secured with phishable MFA (authenticator app) | Mandate **FIDO2 hardware security keys** (YubiKey / Google Titan) for all privileged accounts |
| Single account had unrestricted access to 200 client accounts | Implement **Role-Based Access Control (RBAC)** with strict least-privilege tiers |
| No automated spend anomaly detection in place | Deploy **automated budget spike alerts** with account pause triggers |
| No secondary approval required for mass budget changes | Enforce a **"Two-Man Rule"** for account-wide access or billing modifications |

---

## 📁 Project Documents

Read these in order — they tell the full story from attack to recovery:

| # | Document | Description |
|---|---|---|
| 1 | 📊 [Root Cause Analysis](./JEMSU_Root_Cause_Analysis.md) | Full breakdown of the AiTM attack mechanics, financial impact, and 5 Whys analysis establishing the IAM failure as root cause |
| 2 | 🚨 [Incident Response Playbook](./JEMSU_Incident_Response_Playbook.md) | Step-by-step protocol for identification, containment, eradication, and recovery during an active MCC compromise |
| 3 | ⚡ [Fire Drill Checklist](./JEMSU_Fire_Drill_Checklist.md) | Printable quick-reference checklist for immediate containment — designed for the Ad-Ops team to execute in the first minutes of an incident |
| 4 | 👥 [IAM & RBAC Matrix](./JEMSU_IAM_RBAC_Matrix.md) | Structural guide defining new access tiers, enforcing Principle of Least Privilege across the entire Ad-Ops department |
| 5 | 🔑 [FIDO2 Hardware Key Implementation Guide](./JEMSU_FIDO2_Hardware_Key_Implementation.md) | Step-by-step rollout guide for deploying phishing-resistant hardware security keys and enforcing Zero Trust MFA policy in Google Workspace |

---

## 🛡️ Security Concepts Demonstrated

`Zero Trust Architecture` `Identity & Access Management (IAM)` `Role-Based Access Control (RBAC)`
`Adversary-in-the-Middle (AiTM)` `Phishing-Resistant MFA` `FIDO2 / WebAuthn`
`Principle of Least Privilege (PoLP)` `Incident Response` `Session Hijacking`
`Google Workspace Security` `MFA Enforcement Policy` `Break-Glass Account Management`

---

## 🤳 Connect With Me

[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/c/@zerotrustbro)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/alireza-delsouz)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/zerotrustbro)

---

*"When in doubt, Zero Trust it out."*
