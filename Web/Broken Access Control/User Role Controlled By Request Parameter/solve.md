# Lab 3 – User Role Controlled by Request Parameter

## Lab Link
https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter

---

## Overview

This lab demonstrates a vulnerability where user roles are determined by request parameters.

Attackers can manipulate these parameters to escalate privileges.

---

## Login Credentials

username: wiener  
password: peter

---

## Exploitation Steps

### Step 1 – Intercept Request

Login and intercept the request using **Burp Suite**.

![login](screenshots/login-request.png)

---

### Step 2 – Send Request to Repeater

Send the request to **Burp Repeater**.

---

### Step 3 – Modify Role Parameter

Change:

Admin=false

To:

Admin=true

![modify](screenshots/change-admin.png)

---

### Step 4 – Access Admin Panel

Modify the request line:

GET /admin HTTP/2

---

### Step 5 – Delete User

Find the endpoint:

/admin/delete?username=carlos

Execute:

GET /admin/delete?username=carlos HTTP/2

![delete](screenshots/delete-carlos.png)

---

## Impact

Attackers can escalate privileges and gain administrative access.

---

## Mitigation

- Never trust client-controlled parameters
- Enforce role validation server-side
