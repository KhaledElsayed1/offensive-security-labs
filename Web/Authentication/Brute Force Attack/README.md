# Brute Force Attack

## Overview

A brute force attack is a method used by attackers to guess user credentials by systematically trying multiple password combinations.

Attackers automate login attempts using tools that test thousands of password combinations until the correct password is discovered.

Brute force attacks are commonly used when:

- Password policies are weak
- Login attempts are not limited
- Accounts are not protected by additional security controls

---

# How Brute Force Works

Attackers repeatedly attempt login requests with different password combinations.

Example login request:

```
POST /login
username=carlos
password=123456
```

Attackers use password lists containing commonly used passwords.

Examples include:

```
123456
password
admin
qwerty
letmein
```

---

# Tools Used for Brute Force

Common tools used in brute force attacks include:

- Burp Suite Intruder
- Hydra
- Ncrack
- Medusa

These tools automate login attempts against authentication endpoints.

---

# Attack Scenario

1. The attacker identifies the login endpoint.
2. The attacker intercepts the login request using **Burp Suite**.
3. The attacker sends the request to **Intruder**.
4. The attacker loads a password wordlist.
5. The tool automatically attempts multiple passwords.

If the correct password is found, the attacker gains access to the account.

---

# Impact

Successful brute force attacks can lead to:

- Unauthorized account access
- Account takeover
- Access to sensitive data
- Privilege escalation

---

# Mitigation

Applications should protect against brute force attacks by implementing:

- Rate limiting
- Account lockout after multiple failed attempts
- CAPTCHA verification
- Multi-Factor Authentication (MFA)
- Strong password policies
