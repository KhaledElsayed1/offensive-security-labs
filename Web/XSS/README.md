# Reflected Cross-Site Scripting (XSS)

## Executive Summary

During authorized security testing, a Reflected XSS vulnerability was identified in a web application where user-supplied input was reflected into the HTTP response without proper contextual encoding.

This allowed arbitrary JavaScript execution in the victim's browser within the application’s trust boundary.

---

## Technical Breakdown

The vulnerable endpoint reflects user-controlled parameters directly inside the HTML response.

The application fails to:

- Encode user input before rendering
- Sanitize special characters
- Implement effective CSP restrictions

Payloads were successfully executed in the browser context, confirming client-side code injection capability.

### Example Payload Classes

- Script injection
- Event handler injection
- SVG-based execution
- HTML context breaking

Execution was confirmed via controlled JavaScript proof-of-execution.

---

## Attack Flow

1. Identify reflected parameter.
2. Inject JavaScript payload.
3. Craft malicious URL.
4. Victim loads URL.
5. Browser executes injected code in authenticated context.

---

## Security Impact Analysis

Depending on session configuration and application design, exploitation could enable:

- Session hijacking (if cookies not HttpOnly)
- Token exfiltration via DOM access
- Unauthorized actions via DOM manipulation
- Phishing overlays inside trusted origin
- Account takeover (in chained scenarios)
- Stored attack pivot (if reflected into stored workflow)

Severity varies based on:

- User privilege level
- CSP configuration
- SameSite cookie policy
- Presence of CSRF protections

---

## Risk Classification

- **OWASP Top 10:** A03 – Injection
- **CWE-79:** Improper Neutralization of Input During Web Page Generation
- **Likely CVSS:** Medium–High (context dependent)

---

## Root Cause

The vulnerability exists due to improper output encoding and failure to treat user input as untrusted data.

The application does not perform contextual encoding for:

- HTML body context
- Attribute context
- JavaScript context

---

## Remediation Strategy

Recommended defensive measures:

- Context-aware output encoding
- Strict server-side validation
- Enforced Content Security Policy (CSP)
- HttpOnly & Secure cookie flags
- SameSite cookie configuration
- Security testing before deployment

---

## Evidence

Sanitized proof-of-execution screenshots are included in this repository.  
All identifying information has been redacted to protect confidentiality.

---

## Responsible Disclosure

This finding was identified during authorized testing.  
No sensitive data or production identifiers are disclosed.
