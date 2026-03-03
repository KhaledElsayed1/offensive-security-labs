# Broken Access Control & IDOR

## Overview

Broken Access Control occurs when an application fails to properly enforce restrictions on what authenticated users are allowed to do. 

Access control mechanisms are designed to ensure that users can only access resources and perform actions that they are authorized to perform.

When these controls are improperly implemented, attackers may gain unauthorized access to sensitive data, modify other users' information, or perform privileged actions.

According to **OWASP Top 10**, Broken Access Control is ranked as:

OWASP Top 10 – **A01: Broken Access Control**

This category includes several vulnerabilities such as:

- Insecure Direct Object Reference (IDOR)
- Privilege escalation
- Forced browsing
- Parameter manipulation
- Access control bypass

---

# Access Control Models

## Vertical Access Control

Vertical access control restricts functionality based on **user roles or privilege levels**.

Example roles:

- Administrator
- Moderator
- Normal User

A normal user should not be able to access administrative functionality.

Example restricted endpoint:

```
/admin
/admin/delete-user
/admin/settings
```

If an attacker can access these endpoints without proper authorization checks, this leads to **privilege escalation**.

Example attack:

```
https://example.com/admin
```

If the server does not verify that the user is an administrator, the attacker may gain full administrative access.

---

## Horizontal Access Control

Horizontal access control restricts users from accessing data belonging to other users with the same privilege level.

Example:

A user should only be able to access **their own account information**.

Example request:

```
GET /my-account?id=101
```

If an attacker modifies the identifier:

```
GET /my-account?id=102
```

and gains access to another user's account data, this indicates a **horizontal access control vulnerability**.

---

# Insecure Direct Object Reference (IDOR)

## Definition

IDOR is a specific type of Broken Access Control vulnerability that occurs when applications expose internal object references such as:

- User IDs
- File IDs
- Order numbers
- Database keys

without verifying whether the requesting user is authorized to access the object.

Example vulnerable request:

```
GET /account?id=123
```

If the application only verifies authentication but does not check ownership, attackers can manipulate the identifier.

Example attack:

```
GET /account?id=124
```

This may allow attackers to access another user's private data.

---

# Attack Scenario

1. The attacker logs into the application as a normal user.
2. The attacker observes requests sent to the server using tools such as **Burp Suite**.
3. The attacker identifies parameters referencing internal objects such as:

```
user_id
account_id
order_id
file_id
```

4. The attacker modifies the identifier value.

Example:

```
GET /profile?user_id=1002
```

Modified request:

```
GET /profile?user_id=1003
```

5. If the server returns another user's data, the application is vulnerable to **IDOR**.

---

# Testing Methodology

Security testers often detect IDOR vulnerabilities using the following process.

### Step 1 — Intercept Requests

Use **Burp Suite Proxy** to intercept application traffic.

Look for parameters referencing objects:

```
id=
user=
account=
file=
order=
```

### Step 2 — Modify Object References

Change the identifier value to another number or predictable value.

Example:

```
/api/user/245
```

Modify to:

```
/api/user/246
```

### Step 3 — Analyze the Response

If the server returns another user's data, the application is vulnerable.

Indicators of IDOR include:

- Access to other users’ profiles
- Access to private files
- Exposure of personal information
- Ability to modify other users' resources

---

# Example IDOR Exploit

Original request:

```
GET /api/orders/1254 HTTP/1.1
Host: example.com
Cookie: session=USER_SESSION
```

Modified request:

```
GET /api/orders/1255 HTTP/1.1
Host: example.com
Cookie: session=USER_SESSION
```

If the server returns another user's order information, the application is vulnerable to IDOR.

---

# Impact

Broken Access Control vulnerabilities can lead to serious security consequences.

Possible impacts include:

- Unauthorized access to sensitive user data
- Exposure of personal information
- Account takeover
- Privilege escalation
- Data modification or deletion
- Access to restricted administrative functionality

Because of these risks, Broken Access Control vulnerabilities are considered **high severity**.

---

# Mitigation

To prevent Broken Access Control vulnerabilities, applications should implement the following security measures.

### Enforce Server-Side Authorization

Authorization checks must always be performed on the server.

### Validate Object Ownership

The server must verify that the authenticated user owns the requested resource.

### Use Indirect Object References

Avoid exposing direct database identifiers in URLs.

### Implement Role-Based Access Control (RBAC)

Restrict functionality based on user roles.

### Security Testing

Regular penetration testing and security reviews help detect access control vulnerabilities early.

---

# Key Security Insight

Access control must never rely on **client-side validation**.

All authorization checks should be enforced on the **server side**, and every request must verify that the authenticated user has permission to access the requested resource.

If access control is improperly implemented, attackers can easily manipulate object references and gain unauthorized access to sensitive data.

---

# References

OWASP Top 10 – Broken Access Control  
https://owasp.org/Top10/A01_2021-Broken_Access_Control/

PortSwigger Web Security Academy – Access Control  
https://portswigger.net/web-security/access-control
