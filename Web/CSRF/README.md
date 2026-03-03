# Cross-Site Request Forgery (CSRF)

## Overview

Cross-Site Request Forgery (CSRF) is a web security vulnerability that allows an attacker to trick an authenticated user into performing unintended actions on a web application.

CSRF exploits the trust a server places in a user's browser. If a victim is authenticated, their browser will automatically include session cookies in cross-site requests, enabling unauthorized actions.

- **OWASP Top 10:** A01 – Broken Access Control
- **CWE-352:** Cross-Site Request Forgery

---

## Technical Summary

The vulnerability occurs when:

- A state-changing request (e.g., password change, profile update, transfer action)  
- Does not implement CSRF protection mechanisms  
- And relies solely on session cookies for authentication  

The application accepts authenticated requests without verifying the origin or intent of the request.

---

## Attack Scenario

1. Victim logs into the vulnerable application.
2. Attacker crafts a malicious request (e.g., auto-submitting form).
3. Victim visits attacker-controlled page.
4. The malicious request is automatically sent.
5. The application processes the request using the victim's authenticated session.

---

## Why CSRF Works

Browsers automatically include:

- Session cookies
- Authentication headers (in some contexts)

If no CSRF token or origin validation is implemented, the server cannot distinguish between legitimate and malicious requests.

---

## Impact

Successful exploitation may allow an attacker to:

- Change account passwords
- Modify user email or profile data
- Perform financial transactions
- Trigger administrative actions
- Escalate privileges (in chained scenarios)

Severity depends on:

- Type of affected functionality
- Victim privilege level
- Presence of additional protections (e.g., SameSite cookies)

---

## Root Cause

The vulnerability exists due to:

- Missing anti-CSRF tokens
- No Origin/Referer validation
- Absence of SameSite cookie restrictions
- Reliance on cookie-based authentication without request validation

---

## Proof of Concept

A crafted HTML form was created to replicate a legitimate state-changing request.

When loaded in a browser while the victim was authenticated, the form automatically submitted and executed the targeted action.

All sensitive identifiers and domain names have been redacted in this repository.

---

## Prevention & Mitigation

To prevent CSRF vulnerabilities, applications should implement:

### 1️⃣ Anti-CSRF Tokens
Generate unpredictable, per-session or per-request tokens and validate them server-side.

### 2️⃣ SameSite Cookies
Set cookies as:
- SameSite=Lax
- SameSite=Strict (where possible)

### 3️⃣ Origin & Referer Validation
Verify that state-changing requests originate from trusted domains.

### 4️⃣ Re-authentication for Sensitive Actions
Require password confirmation or MFA for critical operations.

---

## Risk Classification

CSRF is particularly dangerous when:

- Targeting high-privileged accounts
- Combined with XSS
- Affecting financial or administrative functionality

Impact ranges from Medium to Critical depending on context.

---

## Responsible Disclosure

This case study documents testing performed in authorized environments.

All target identifiers and sensitive information have been removed to protect confidentiality.
