# Cross-Site Scripting (XSS)

## Overview

Cross-Site Scripting (XSS) is a client-side injection vulnerability that allows an attacker to execute arbitrary JavaScript in a victim’s browser within the trusted context of a web application.

XSS occurs when an application includes untrusted data in a web page without proper validation or contextual output encoding.

XSS is classified under:

- **OWASP Top 10 – A03: Injection**
- **CWE-79: Improper Neutralization of Input During Web Page Generation**

---

# Types of XSS

XSS vulnerabilities are generally categorized into three main types:

1. Reflected XSS
2. Stored XSS
3. DOM-Based XSS

---

## 1️⃣ Reflected XSS

### Definition

Reflected XSS occurs when user input is immediately returned (reflected) in the HTTP response without proper sanitization.

The malicious payload is not stored on the server. Instead, it is embedded in a crafted request (usually via URL parameters).

### Attack Flow

1. Attacker injects malicious script into a request parameter.
2. Victim clicks a specially crafted link.
3. The server reflects the payload in the response.
4. The browser executes the injected script.

### Common Locations

- Search parameters
- Error messages
- Form submissions
- Redirect URLs

### Risk Level

Medium to High (depending on context and user privilege).

---

## 2️⃣ Stored XSS (Persistent XSS)

### Definition

Stored XSS occurs when malicious input is stored on the server (e.g., database) and later served to users without proper encoding.

This is more dangerous than Reflected XSS because it does not require user interaction beyond visiting the affected page.

### Attack Flow

1. Attacker submits malicious payload.
2. The application stores it (e.g., comment, message, profile field).
3. Other users load the page.
4. The payload executes automatically.

### Common Locations

- Comment systems
- Chat messages
- User profiles
- Feedback forms
- Admin dashboards

### Risk Level

High to Critical (especially if executed in admin context).

---

## 3️⃣ DOM-Based XSS

### Definition

DOM-Based XSS occurs when the vulnerability exists entirely on the client side.

The server response itself may be safe, but client-side JavaScript reads user-controlled input and dynamically injects it into the DOM without proper sanitization.

### Key Difference

- Reflected & Stored XSS → Vulnerability originates from server response.
- DOM XSS → Vulnerability originates from client-side JavaScript logic.

### Attack Flow

1. Attacker manipulates a URL fragment or client-controlled input.
2. JavaScript processes it.
3. Data is written to the DOM unsafely.
4. The payload executes in the browser.

### Common Sources (DOM)

- `document.location`
- `document.URL`
- `document.referrer`
- `window.name`

### Common Sinks

- `innerHTML`
- `document.write`
- `eval`
- `setTimeout(string)`
- `setInterval(string)`

### Risk Level

Medium to High (depends on execution context).

---

# Impact of XSS

Successful exploitation may allow attackers to:

- Execute arbitrary JavaScript
- Steal session tokens (if not HttpOnly)
- Perform actions on behalf of users
- Modify page content dynamically
- Conduct phishing attacks within trusted origin
- Escalate privileges (in chained attacks)
- Capture sensitive DOM data

Impact severity depends on:

- Cookie configuration (HttpOnly / Secure / SameSite)
- CSP implementation
- Victim privilege level
- Application functionality

---

# Root Causes

XSS vulnerabilities typically occur due to:

- Lack of contextual output encoding
- Insufficient input validation
- Unsafe DOM manipulation
- Absence of Content Security Policy
- Treating user input as trusted data

---

# Prevention Strategies

Effective mitigation requires a layered defense approach:

### 1️⃣ Contextual Output Encoding
Encode output depending on context:
- HTML body
- HTML attribute
- JavaScript context
- URL context

### 2️⃣ Input Validation
Validate input on server side using strict allowlists.

### 3️⃣ Content Security Policy (CSP)
Implement strict CSP to reduce exploitation impact.

### 4️⃣ Secure Cookie Configuration
- HttpOnly
- Secure
- SameSite

### 5️⃣ Avoid Dangerous DOM APIs
Avoid using:
- innerHTML
- eval
- document.write

Use safe alternatives like:
- textContent
- createElement
- setAttribute

---

# Summary Comparison

| Type        | Stored on Server | Requires User Interaction | Execution Location | Severity |
|------------|------------------|--------------------------|-------------------|----------|
| Reflected  | No               | Yes                      | Server response   | Medium–High |
| Stored     | Yes              | No                       | Server response   | High–Critical |
| DOM-Based  | No               | Yes (usually)            | Client-side JS    | Medium–High |

---

# Responsible Usage

All testing and demonstrations in this repository were conducted in authorized environments.

No production systems or sensitive identifiers are disclosed.
