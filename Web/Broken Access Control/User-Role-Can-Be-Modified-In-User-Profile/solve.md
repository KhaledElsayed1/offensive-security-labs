# Lab 4 – User Role Can Be Modified in User Profile

## Lab Link
https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile

---

## Overview

This lab demonstrates a Broken Access Control vulnerability where the application allows users to modify sensitive parameters in their profile update request.

By manipulating the `roleid` parameter in the request, an attacker can escalate their privileges and gain administrative access.

The goal of this lab is to exploit this vulnerability to gain admin privileges and delete the user **carlos**.

---

## Login Credentials

username: wiener  
password: peter

---

## Step 1 – Login to the Application

Login using the provided credentials and navigate to the **My Account** page.

![login](screenshots/login.png)

---

## Step 2 – Update Email Address


Change the email address to any value such as:# Lab 4 – User Role Can Be Modified in User Profile

## Lab Link
https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile

---

## Overview

This lab demonstrates a Broken Access Control vulnerability where the application allows users to modify sensitive parameters in their profile update request.

By manipulating the `roleid` parameter in the request, an attacker can escalate their privileges and gain administrative access.

The goal of this lab is to exploit this vulnerability to gain admin privileges and delete the user **carlos**.

---

## Login Credentials

username: wiener  
password: peter

---

## Step 1 – Login to the Application

Login using the provided credentials and navigate to the **My Account** page.

![login](screenshots/login.png)

---

## Step 2 – Update Email Address

Change the email address to any value such as: test@test.com

Intercept the request using **Burp Suite**.

![change-email](screenshots/change-email.png)

---

## Step 3 – Send Request to Repeater

Send the intercepted request to **Burp Repeater** in order to modify its parameters.

![repeater](screenshots/send-to-repeater.png)

---

## Step 4 – Modify Role ID

Inside the request body, add the following parameter: "roleid":2


Example request body: {
"email":"test@test.com
",
"roleid":2
}

This modification changes the user's role to **administrator**.

![role-modification](screenshots/roleid.png)

---

## Step 5 – Access Admin Panel

After modifying the role, navigate to: /admin

The admin panel becomes accessible.

![admin-panel](screenshots/admin-panel.png)

---

## Step 6 – Delete Target User

Locate the user **carlos** and delete the account.

![delete-carlos](screenshots/delete-carlos.png)

---

## Impact

This vulnerability allows attackers to escalate privileges by manipulating user-controlled parameters.

Possible consequences include:

- Privilege escalation
- Unauthorized administrative access
- User account manipulation
- Data compromise

---

## Mitigation

To prevent this issue:

- Never trust client-side parameters
- Enforce server-side role validation
- Implement strict authorization checks
- Restrict sensitive parameters from user requests

---

## Conclusion

This lab highlights how improper validation of user profile parameters can lead to privilege escalation vulnerabilities.








