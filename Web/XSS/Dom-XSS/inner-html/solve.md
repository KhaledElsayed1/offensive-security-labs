## DOM XSS in `innerHTML` Sink

### Lab Overview
This lab demonstrates a **DOM-based Cross-Site Scripting (DOM XSS)** vulnerability caused by inserting **user-controlled input** into the page using the `innerHTML` property.

The application reads the value of the **search parameter from the URL** and dynamically inserts it into the page using `innerHTML` without sanitization. Because `innerHTML` interprets the inserted content as **HTML markup**, attackers can inject malicious HTML or JavaScript that executes in the victim’s browser.

---

## Vulnerability Explanation

### What is DOM XSS?

DOM-based Cross-Site Scripting occurs when:

1. JavaScript reads **untrusted data** from a source controlled by the user.
2. The data is passed into a **dangerous DOM sink**.
3. The data is inserted into the page **without sanitization or escaping**.

Unlike reflected XSS, the attack happens **entirely in the browser** and never reaches the server.

---

## Source

In this lab the attacker-controlled input comes from:

location.search


Example URL:

https://example.com/?search=test


The `search` parameter can be manipulated by the attacker.

---

## Sink

The vulnerable sink used in this lab is:

javascript
element.innerHTML
Example vulnerable code:

var search = location.search.substring(1);
document.getElementById("searchMessage").innerHTML =
"Search results for: " + search;
Here the application inserts user input directly into the page using innerHTML.

Why innerHTML is Dangerous
innerHTML treats inserted content as HTML markup.

If attacker-controlled data is inserted into it, the browser will parse and render it as real HTML.

Example:

element.innerHTML = userInput;
If the attacker supplies:

<img src=x onerror=alert(1)>
The browser will execute the JavaScript inside the onerror attribute.

Lab Goal
The goal of the lab is to execute JavaScript in the browser using a DOM XSS payload.

Once the payload triggers alert(1), the lab will be marked as solved.

Exploitation Steps
1. Open the Lab
Open the lab page and observe the search feature.

Example URL:

https://LAB-ID.web-security-academy.net/?search=test
2. Inspect the JavaScript Code
Inspect the page source or developer tools.

You will find code similar to:

document.getElementById("searchMessage").innerHTML =
"Search results for: " + query;
This indicates that the search parameter is inserted directly into the DOM.

3. Craft the Payload
Because innerHTML parses HTML, we can inject an HTML element that executes JavaScript.

Payload:

<img src=x onerror=alert(1)>
4. Send the Exploit
Insert the payload into the search parameter:

https://LAB-ID.web-security-academy.net/?search=<img src=x onerror=alert(1)>
5. Trigger the XSS
When the page loads:

The browser reads the search parameter.

The JavaScript inserts it into the DOM using innerHTML.

The browser parses the injected HTML.

The onerror event executes JavaScript.

Result:

alert(1)
The alert appears and the lab is solved.

Root Cause
The vulnerability occurs because:

The application reads user input from the URL

The input is inserted into the page using innerHTML

No HTML escaping or sanitization is applied

Security Impact
If exploited in a real-world application, attackers could:

Execute arbitrary JavaScript

Steal session cookies

Perform actions on behalf of users

Inject malicious content

Launch phishing attacks

Prevention
1. Avoid innerHTML with Untrusted Data
Do not insert user input directly using:

innerHTML
outerHTML
document.write()
2. Use Safe DOM APIs
Use:

textContent
instead of:

innerHTML
Example:

element.textContent = userInput;
This ensures the browser treats the content as plain text, not HTML.

3. Sanitize User Input
Use a trusted library such as:

DOMPurify
Example:

element.innerHTML = DOMPurify.sanitize(userInput);
4. Implement Content Security Policy
Example CSP:

Content-Security-Policy: script-src 'self'
This can help mitigate some XSS attacks.

Key Takeaway
DOM XSS occurs when attacker-controlled input from the browser is inserted into the DOM using unsafe JavaScript sinks without sanitization.

In this lab the vulnerability chain was:

Source → location.search
Sink → innerHTML
By injecting malicious HTML into the URL, we were able to execute JavaScript and successfully solve the lab.
