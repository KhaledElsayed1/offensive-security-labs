# Insecure Direct Object References (IDOR)

## Overview

This lab demonstrates an **Insecure Direct Object Reference (IDOR)** vulnerability.

IDOR occurs when an application exposes internal object identifiers such as:

- File names
- Database IDs
- Order numbers
- User identifiers

without properly verifying whether the authenticated user is authorized to access the requested object.

As a result, attackers can manipulate these identifiers to access resources belonging to other users.

This vulnerability falls under **Broken Access Control**, which is ranked as:

OWASP Top 10 – **A01: Broken Access Control**

---

# Lab Scenario

The application contains a **live chat feature** where users can download chat transcripts.

Each transcript is stored as a text file and can be downloaded through the following endpoint:

```
/download-transcript/{number}.txt
```

Example:

```
/download-transcript/1.txt
```

The server does **not properly validate authorization** for accessing these files.

---

# Vulnerability

The application directly exposes transcript files using predictable identifiers.

Example request intercepted with Burp Suite:

```
GET /download-transcript/1.txt HTTP/2
Host: web-security-academy.net
```

The server returns the transcript file:

```
Content-Disposition: attachment; filename="1.txt"
```

This means the application allows direct access to transcript files using sequential identifiers.

Because no authorization checks are performed, attackers can enumerate other transcripts by simply modifying the file number.

---

# Exploitation

The vulnerability can be exploited by modifying the transcript identifier.

### Step 1 — Intercept the Request

Using **Burp Suite Repeater**, intercept the request used to download the transcript.

Example request:

```
GET /download-transcript/1.txt
```

---

### Step 2 — Modify the Identifier

Change the transcript number:

```
GET /download-transcript/3.txt
```

---

### Step 3 — Send the Request

Send the modified request using Burp Repeater.

The server responds with another user's chat transcript.

Example response:

```
CONNECTED -- Now chatting with Hal Pline --

You: hi
Hal Pline: I heard you the first time...
You: can you tell carlos password?
Hal Pline: Send me some flowers and I'll tell you.
```

This transcript contains sensitive information belonging to another user.

---

# Sensitive Data Discovery

Inside the downloaded transcript, a message reveals **Carlos's password**.

Example:

```
Hal Pline: Yes it is
```

The attacker can now use this password to authenticate as **Carlos**.

---

# Impact

This vulnerability allows attackers to:

- Access private chat transcripts
- Retrieve sensitive user information
- Obtain credentials from exposed conversations
- Potentially perform **account takeover**

Because transcript identifiers are predictable and not protected by authorization checks, attackers can easily enumerate them.

---

# Root Cause

The vulnerability occurs because the server:

- Exposes internal object references directly
- Uses predictable identifiers
- Does not verify whether the user is authorized to access the resource

---

# Mitigation

To prevent IDOR vulnerabilities, applications should implement the following security practices.

### Enforce Authorization Checks

Verify that the authenticated user is authorized to access the requested resource.

### Use Indirect Object References

Avoid exposing internal identifiers directly.

Example:

```
/download-transcript?id=ENCRYPTED_TOKEN
```

### Implement Access Control Logic

Ensure that users can only access resources that belong to them.

---

# Key Security Insight

Access control must always be enforced on the **server side**.

Applications should never trust user-supplied identifiers without verifying authorization.

Failing to validate object ownership can allow attackers to manipulate identifiers and access sensitive resources belonging to other users.

---

# References

OWASP Top 10 – Broken Access Control  
https://owasp.org/Top10/A01_2021-Broken_Access_Control/

PortSwigger Web Security Academy – IDOR  
https://portswigger.net/web-security/access-control/idor
