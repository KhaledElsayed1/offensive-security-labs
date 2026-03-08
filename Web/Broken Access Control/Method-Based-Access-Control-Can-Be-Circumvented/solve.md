# Lab 6 – Method-Based Access Control Can Be Circumvented

## Lab Link
https://portswigger.net/web-security/access-control/lab-method-based-access-control-can-be-circumvented

---

## Overview

This lab demonstrates a vulnerability where access control depends on the HTTP request method.

The application restricts certain operations when using one method but fails to enforce the same restrictions when the method changes.

By changing the request method, attackers can bypass access control.

---

## Step 1 – Login as Administrator

Login using the following credentials:

username: administrator  
password: admin

![login](screenshots/login.png)

---

## Step 2 – Access Admin Panel

Navigate to the admin panel. /admin

![admin](screenshots/admin-panel.png)

---

## Step 3 – Capture Role Modification Request

Capture the request used to modify user roles using **Burp Suite**.

Send it to **Burp Repeater**.

![request](screenshots/request.png)

---

## Step 4 – Change Request Method

Right-click the request and choose: Change request method → GET

![method-change](screenshots/change-method.png)

---

## Step 5 – Modify Username

Change the username parameter from: carlos

to => wiener

Send the request again.

![modify](screenshots/modify-username.png)

---

## Final Result

The request successfully modifies the user's role and the lab is solved.

![solved](screenshots/lab-solved.png)

---

## Impact

Attackers can bypass access control by manipulating HTTP methods.

This may lead to:

- Privilege escalation
- Unauthorized administrative actions
- Data compromise

---

## Mitigation

To mitigate this vulnerability:

- Apply access control checks regardless of HTTP method
- Implement consistent authorization logic
- Validate requests on the server side








