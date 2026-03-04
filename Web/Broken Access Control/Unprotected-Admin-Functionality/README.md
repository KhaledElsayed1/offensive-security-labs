# Unprotected Admin Functionality (Broken Access Control)

## Vulnerability Overview

**Unprotected Admin Functionality** is a Broken Access Control issue where administrative endpoints (admin panel / admin actions) are accessible without proper authorization checks.

In a secure design:
- Admin pages must be protected by **authentication** (who you are)
- And **authorization** (what you are allowed to do)

When an application only hides the admin URL (security by obscurity) or forgets to enforce server-side authorization, any user who discovers the endpoint can access it and perform sensitive actions.

**Common discovery sources:**
- `robots.txt`
- Page source / JavaScript files
- Directory enumeration
- Predictable paths like `/admin`, `/administrator`, `/admin-panel`

---

## Lab Information

- **Platform:** PortSwigger Web Security Academy  
- **Lab Name:** Unprotected admin functionality  
- **Category:** Broken Access Control  
- **Goal:** Access the admin interface and delete the user **carlos**.

---

## Exploitation Walkthrough (How I Solved It)

### 1) Finding Hidden Admin Path

I started with content discovery and checked `robots.txt`:

- Visited:
  - `/robots.txt`

The file revealed a disallowed admin endpoint similar to:

```
User-agent: *
Disallow: /administrator-panel
```

This is a common real-world issue: developers sometimes list sensitive endpoints in `robots.txt` to hide them from search engines, but it still exposes the path to attackers.

---

### 2) Accessing the Admin Panel

After identifying the path, I navigated directly to:

- `/administrator-panel`

Because the endpoint was not protected by authorization controls, it was accessible without admin privileges.

---

### 3) Performing the Admin Action

Inside the admin panel, there was a user management feature.
I used it to delete the target user:

- Deleted user: **carlos**

After deleting the user, the lab was marked as **Solved**.

---


## Impact

If this occurred in a real application, an attacker could:

- Access admin dashboards
- Delete users
- Modify data and settings
- Escalate privileges
- Fully compromise the application

---

## Mitigation

- Enforce **server-side authorization** on every admin endpoint
- Use role-based access control (RBAC) or attribute-based access control (ABAC)
- Avoid relying on hidden URLs for security
- Monitor and alert on unauthorized admin endpoint access
- Keep sensitive paths out of `robots.txt` (or assume attackers will read it anyway)
