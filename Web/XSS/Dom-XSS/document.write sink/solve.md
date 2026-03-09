 🧪 PortSwigger Lab: DOM XSS in `document.write` sink using `location.search` inside a `<select>` element

## 📖 Lab Concept
This lab demonstrates a **DOM-based Cross-Site Scripting (XSS)** vulnerability.  
The page dynamically populates a `<select>` element using data taken directly from the **`location.search`** (the query string in the URL).  
The script uses **`document.write()`** to insert this data into the DOM without any sanitization or encoding, which makes it exploitable.

---

## ⚙️ Vulnerable Code
```javascript
var pos = location.search.indexOf("default=");
if (pos != -1) {
    var defaultOption = location.search.substring(pos+8);
    document.write("<select><option>" + defaultOption + "</option></select>");
}
The value after default= in the URL is directly written into the page.

No validation or escaping is applied, so injected HTML/JavaScript will execute.

🚨 Exploitation Steps
Open the lab in your browser.

Add a malicious payload to the query string, for example:

Code
?default=<img src=x onerror=alert(1)>
The script reads the value after default= and writes it into the DOM using document.write.

The injected JavaScript executes, proving the XSS vulnerability.

✅ Example Payload
text
?default=<img src=x onerror=alert(document.domain)>
This payload triggers an alert showing the current domain, confirming successful exploitation.

🛡️ Mitigation Notes
Avoid using document.write() entirely.

Use safe DOM APIs like textContent or innerText instead of innerHTML.

Apply proper HTML encoding to user input before inserting it into the DOM.

Consider libraries such as DOMPurify to sanitize untrusted input.

Implement a strong Content Security Policy (CSP) to reduce XSS impact.
