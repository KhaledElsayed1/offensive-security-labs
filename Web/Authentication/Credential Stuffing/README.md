# Credential Stuffing

## Overview

Credential stuffing is an attack where attackers use stolen username and password combinations from previous data breaches to gain unauthorized access to user accounts.

Many users reuse the same passwords across multiple websites.

If attackers obtain leaked credentials from one breach, they can attempt to log in to other services using the same credentials.

---

# How Credential Stuffing Works

Attackers obtain leaked credentials from:

- Data breaches
- Dark web marketplaces
- Public leak databases

Example leaked credentials:

```
carlos@example.com : password123
user1@gmail.com : qwerty
admin@test.com : letmein
```

Attackers then automate login attempts using these credentials.

---

# Attack Tools

Common tools used for credential stuffing include:

- Sentry MBA
- Snipr
- OpenBullet
- Burp Suite

These tools allow attackers to test thousands of credential pairs against login endpoints.

---

# Attack Scenario

1. The attacker obtains a list of leaked credentials.
2. The attacker targets a login endpoint.
3. Automated tools attempt login using credential pairs.
4. If credentials are reused, the attacker gains access to accounts.

---

# Impact

Credential stuffing attacks can lead to:

- Account takeover
- Exposure of sensitive data
- Unauthorized transactions
- Financial fraud

Because these attacks use valid credentials, they can be difficult to detect.

---

# Mitigation

Applications should protect against credential stuffing by implementing:

- Multi-Factor Authentication (MFA)
- Rate limiting
- Detection of abnormal login behavior
- Monitoring login attempts from multiple IP addresses
- Preventing password reuse
