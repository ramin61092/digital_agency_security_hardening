JEMSU Ad-company Security Engagement: Incident Response & IAM Hardening
Author: Ramin

Date: January 2026

Status: Post-Incident Remediation & Policy Generation

Advisory Disclaimer
This repository contains independent consulting documentation, methodologies, and recommended best practices for mitigating an account compromise and malvertising event. It is not an official JEMSU document and does not necessarily reflect JEMSU’s internal policies, existing security posture, or standard operating procedures. All structures, including the Role-Based Access Control (RBAC) matrix, are theoretical models designed to illustrate Zero Trust principles based on external findings.

Executive Summary
This repository documents the incident response, root cause analysis, and subsequent security hardening strategies following a major data breach within the JEMSU Digital Advertising division.

A sophisticated Adversary-in-the-Middle (AiTM) spear-phishing campaign targeted the Director of Digital Advertising, successfully bypassing standard Multi-Factor Authentication (MFA) to steal an active session token. The threat actors leveraged this compromised "Global Admin" access within the Google Ads Manager Account (MCC) to deploy malvertising payloads across 200 client accounts, resulting in approximately over $100,000 USD in unauthorized ad spend before containment.

Project Objectives
The primary goals of this security engagement are to:

Analyze the Attack Vector: Detail how the AiTM attack bypassed existing MFA protocols.

Contain and Remediate: Provide an immediate playbook to halt financial loss and expel the threat actors.

Restructure Identity & Access Management (IAM): Eliminate standing administrative privileges by implementing a Zero Trust and Principle of Least Privilege (PoLP) architecture.

Fortify Human Defense: Deploy specialized training to the Ad-Ops team to recognize high-level, admin-targeted social engineering lures.

Key Findings & Core Recommendations
Critical Vulnerability: Over-privileged administrative accounts secured with phishable MFA (authenticator apps/SMS).

Immediate Remediation: Mandatory deployment of FIDO2 hardware security keys (e.g., YubiKey) for all personnel with MCC access to physically block session-hijacking.

Structural Remediation: Disaggregation of "Global Admin" roles into segmented, segmented client-access tiers, enforcing a "Two-Man Rule" for overarching budget or user access modifications.

Repository Structure & Documentation
This repository contains the following artifacts generated for the JEMSU executive and technical teams:

docs/
01_Root_Cause_Analysis.md - A detailed breakdown of the AiTM attack mechanics, the financial impact spread, and the "5 Whys" establishing the IAM failure.

02_Incident_Response_Playbook.md - The "Fire Drill" protocol for immediate containment, session invalidation, and recovery during an active MCC compromise.

03_Security_Awareness_Training.md - A specialized curriculum for digital advertising teams focusing on domain spoofing, fake MCC invites, and safe asset handling.

04_IAM_and_RBAC_Matrix.md - A structural guide defining new access levels, enforcing the Principle of Least Privilege across the Ad-Ops department.

05_Hardware_Key_Setup_Guide.md - (Pending) Step-by-step implementation for FIDO2 enforcement.

06_Client_Breach_Notification.md - (Pending) External crisis communication template for the 200 affected clients.
