# Lab 5 – URL-Based Access Control Can Be Circumvented

## Lab Link
https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented

---

## Overview

This lab demonstrates a vulnerability where access control is implemented based on URL paths, but the backend trusts certain HTTP headers.

By manipulating the `X-Original-URL` header, attackers can bypass access control restrictions and access restricted resources.

The objective of this lab is to exploit this misconfiguration and delete the user **carlos**.

---

## Step 1 – Attempt to Access the Admin Panel

Navigate to the following endpoint: /admin

The server returns **403 Forbidden**, indicating that access is restricted.

![403](screenshots/403.png)

---

## Step 2 – Intercept the Request

Capture the request using **Burp Suite**.

Send the request to **Repeater**.

![intercept](screenshots/intercept.png)

---

## Step 3 – Bypass Access Control

Add the following HTTP header: X-Original-URL: /admin

Send the request again.

The server processes the request as if it was accessing `/admin`.

![header-bypass](screenshots/header-bypass.png)

---

## Step 4 – Delete Target User

Modify the request as follows:

Request line: GET /?username=carlos HTTP/2

Header: X-Original-URL: /admin/delete

Send the request.

![delete](screenshots/delete-carlos.png)

---

## Impact

Attackers can bypass access control mechanisms and access restricted administrative functionality.

Possible consequences include:

- Unauthorized admin access
- Data manipulation
- User deletion
- Privilege escalation

---

## Mitigation

To prevent this vulnerability:

- Do not trust client-controlled headers
- Implement strict server-side access control
- Validate user permissions before processing requests








