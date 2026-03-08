# DOM-Based Cross-Site Scripting (DOM XSS)

## Overview
DOM-based Cross-Site Scripting (DOM XSS) is a type of Cross-Site Scripting vulnerability where the attack is executed entirely on the client side. Unlike traditional XSS (Stored or Reflected), the malicious payload never reaches the server. Instead, the vulnerability occurs when JavaScript running in the browser processes untrusted data and writes it into the Document Object Model (DOM) without proper sanitization.

---

## How DOM XSS Works
DOM XSS occurs when:

1. The application reads data from a **source** controlled by an attacker.
2. The data is passed to a **sink** that executes JavaScript or interprets HTML.
3. The data is not properly sanitized or encoded before insertion into the DOM.

---

## Common Sources
- window.location`, `window.location.href`, `window.location.search`, `window.location.hash`
- document.referrer`
- document.cookie`
- localStorage`, `sessionStorage`
- postMessage`

```javascript
let query = window.location.search;
Common Sinks
innerHTML, outerHTML

document.write(), document.writeln()

eval(), setTimeout(), setInterval()

location

element.src, element.href

document.getElementById("output").innerHTML = userInput;
Example of a DOM XSS Vulnerability
Vulnerable Code
let name = window.location.hash.substring(1);
document.getElementById("welcome").innerHTML = "Hello " + name;
Malicious URL
https://example.com/#<script>alert(1)</script>
Result
The script is injected into the DOM and executed by the browser.

Impact
Execute arbitrary JavaScript in the victim's browser

Steal session cookies

Perform actions on behalf of the victim

Modify page content

Deliver phishing interfaces

Account takeover attacks

Detection Techniques
Manual Testing
Inspect JS code for unsafe DOM manipulations.

Payload Injection
Inject common XSS payloads into URL parameters or fragments:

#<img src=x onerror=alert(1)>
Browser Developer Tools
Monitor DOM changes and JS execution.

Automated Tools
Burp Suite

DOM Invader

XSStrike

DalFox

Prevention and Mitigation
1. Avoid Dangerous Sinks
Avoid innerHTML, document.write(), eval() with user input.

2. Use Safe Alternatives
element.textContent = userInput; // safer alternative
3. Input Sanitization
Use libraries like DOMPurify:

let clean = DOMPurify.sanitize(userInput);
element.innerHTML = clean;
4. Content Security Policy (CSP)
Implement strong CSP:

Content-Security-Policy: script-src 'self';
Real-World Attack Scenario
Attacker finds page reading window.location.hash.

The value is inserted into innerHTML without sanitization.

Attacker crafts malicious URL with JS payload.

Victim opens the link.

Script executes → successful DOM XSS.
