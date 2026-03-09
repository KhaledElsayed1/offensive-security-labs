## DOM XSS in document.write Sink

### Lab Overview
This lab demonstrates a **DOM-based Cross-Site Scripting (DOM XSS)** vulnerability caused by the use of the `document.write()` function with **unsanitized user input**.

In this scenario, the application reads data directly from the **URL query string** and writes it into the HTML document using `document.write()` without performing any validation or sanitization.  
Because the data is inserted directly into the DOM, an attacker can inject malicious JavaScript code that will execute in the victim’s browser.

---

## Vulnerability Explanation

### What is DOM XSS?
DOM-based XSS occurs when **JavaScript running in the browser takes untrusted data from a controllable source and writes it into a dangerous sink without proper sanitization**.

Unlike reflected or stored XSS, the payload is **never processed by the server**.  
Instead, the vulnerability exists entirely in the **client-side JavaScript**.

---

### Source
In this lab, the attacker-controlled input comes from the URL: location.search
Example:
https://example.com/?search=test


The `search` parameter is controlled by the user.

---

### Sink

The vulnerable sink used in this lab is:
javascript
document.write()
Example vulnerable code:

var query = location.search;
document.write('<img src="/resources/images/tracker.gif?search=' + query + '">');
Here the application writes the query parameter directly into the page without escaping it.

Why document.write() is Dangerous
document.write() directly injects HTML into the page.
If user input is inserted inside it, attackers can break out of the intended context and inject malicious code.

Example:

<script>
document.write(userInput);
</script>
If userInput contains:

<script>alert(1)</script>
The browser will execute the injected script.

Lab Goal
The goal of this lab is to trigger a JavaScript alert using DOM-based XSS by exploiting the document.write() sink.

When the alert executes, the lab is marked as solved.

Exploitation Steps
1. Open the Lab
Open the lab in the browser and observe the search functionality.

Example URL:

https://LAB-ID.web-security-academy.net/?search=test
2. Inspect the Page Source
View the page source or inspect the JavaScript code.

You will notice a script similar to:

document.write('<img src="/resources/images/tracker.gif?search=' + location.search + '">');
This shows that the application writes the query string directly into the DOM.

3. Craft the Payload
To exploit the vulnerability, we must break out of the HTML attribute and inject a script.

Payload:

"><svg onload=alert(1)>
4. Send the Exploit URL
Append the payload to the search parameter:

https://LAB-ID.web-security-academy.net/?search="><svg onload=alert(1)>
5. Trigger the XSS
When the page loads:

The JavaScript reads the query string.

It passes the value to document.write().

The browser interprets the injected payload as HTML.

The svg tag executes the onload event.

Result:

alert(1)
The alert pops up and the lab is solved.

Root Cause
The vulnerability exists because:

The application reads user-controlled data from the URL

The data is passed directly to a dangerous DOM sink

No escaping or sanitization is performed before writing to the DOM

Security Impact
If exploited in a real application, this vulnerability could allow attackers to:

Steal user session cookies

Perform actions on behalf of the victim

Deface the webpage

Inject malicious scripts

Perform phishing attacks

Prevention
To prevent DOM XSS vulnerabilities:

1. Avoid Dangerous Sinks
Do not use:
document.write()
innerHTML
outerHTML
eval()

3. Sanitize User Input
Use proper escaping before inserting data into the DOM.

Example:

element.textContent = userInput;
instead of: element.innerHTML = userInput;

3. Use Secure Frameworks
Modern frameworks like:
React
Angular
Vue

automatically escape HTML content by default.

4. Implement Content Security Policy (CSP)
A strong CSP can help mitigate XSS attacks by restricting script execution.

Example:

Content-Security-Policy: script-src 'self'
Key Takeaway
DOM XSS occurs when attacker-controlled input from the browser is written into the DOM using unsafe JavaScript sinks without sanitization.

In this lab, the vulnerability was caused by:

Source → location.search
Sink → document.write()
By injecting a malicious payload into the URL, we were able to execute arbitrary JavaScript and successfully solve the lab.
