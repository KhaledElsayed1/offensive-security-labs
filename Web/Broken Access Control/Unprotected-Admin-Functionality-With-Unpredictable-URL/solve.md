# Lab 2 – Unprotected Admin Functionality with Unpredictable URL

## Lab Link
https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url

---

## Overview

This lab demonstrates how security through obscurity fails when administrative endpoints are hidden using unpredictable URLs but not protected by proper authorization.

The objective is to discover the hidden admin URL and delete the user **carlos**.

---

## Reconnaissance

Open the lab homepage and inspect the page source.

Press:

CTRL + U

Search for hidden paths.

The following endpoint appears:

/admin-aame8y

![source](screenshots/source-code.png)

---

## Exploitation

Navigate to the discovered endpoint:

https://LAB-ID.web-security-academy.net/admin-aame8y

The administrative interface becomes accessible.

![admin](screenshots/admin-interface.png)

---

## Delete Target User

Locate user:

carlos

Click delete.

![delete](screenshots/delete-carlos.png)

---

## Impact

Hidden URLs do not provide security. Attackers can easily discover endpoints through source code analysis or automated scanning.

---

## Mitigation

- Implement authentication checks
- Avoid relying on hidden URLs for protection
- Apply server-side access control verification
