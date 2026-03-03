# Username Enumeration

## Overview

Username Enumeration occurs when an application reveals whether a username exists in the system during the authentication process.

This vulnerability allows attackers to identify valid usernames by analyzing differences in server responses during login attempts.

Once attackers obtain a list of valid usernames, they can perform further attacks such as:

- Brute force attacks
- Credential stuffing
- Targeted password guessing

Username Enumeration is often the **first step in many account takeover attacks**.

---

# How Username Enumeration Happens

Applications may respond differently depending on whether the username exists or not.

Example responses:

Invalid username

Incorrect password

If the attacker enters a valid username but the wrong password, the application may return a different message than when the username does not exist.

These differences allow attackers to determine valid usernames.

---

# Example Attack

Login request:

```
POST /login
username=carlos
password=test123
```

Possible responses:

```
Invalid username
```

vs

```
Incorrect password
```

If the response changes depending on the username, attackers can enumerate valid users.

---

# Testing Methodology

Security testers detect username enumeration by analyzing server responses.

Steps include:

1. Intercept login requests using **Burp Suite Proxy**.
2. Send multiple login attempts with different usernames.
3. Observe differences in:
   - Error messages
   - HTTP status codes
   - Response length
   - Response time

These differences may indicate valid usernames.

---

# Impact

Username Enumeration helps attackers:

- Discover valid accounts
- Launch targeted brute force attacks
- Perform credential stuffing attacks
- Prepare account takeover attempts

---

# Mitigation

Applications should prevent username enumeration by:

- Returning identical error messages for all login failures
- Avoiding response differences between valid and invalid usernames
- Implementing rate limiting on login attempts
- Using CAPTCHA protection
