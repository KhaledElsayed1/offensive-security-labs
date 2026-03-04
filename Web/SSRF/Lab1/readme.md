# Lab: Basic SSRF Against Another Back-End System

## Lab Overview

This lab demonstrates a **Server-Side Request Forgery (SSRF)** vulnerability in a stock checking feature.

The application fetches stock information from a URL supplied by the user. Because the URL is not properly validated, the attacker can make the server send requests to internal systems.

---

## Lab Objective

The goal of this lab is to:

1. Use the stock check feature to scan the internal network
2. Identify the internal admin interface
3. Access the admin panel
4. Delete the user **carlos**

---

## Identifying the Vulnerable Parameter

Intercept the stock check request using **Burp Suite**.

Example request:

```
POST /product/stock HTTP/2
Host: vulnerable-lab.com

stockApi=http://example.com
```

The parameter `stockApi` is used by the server to fetch remote data.

---

## Testing for SSRF

Replace the external URL with an internal address.

Example:

```
stockApi=http://127.0.0.1
```

or

```
stockApi=http://192.168.0.1:8080
```

If the server returns a response, this indicates that the server is making the request internally.

---

## Scanning the Internal Network

Use **Burp Intruder** to scan the internal network range.

Target:

```
192.168.0.§1§:8080
```

Payload range:

```
1 → 254
```

Monitor the responses and look for differences in:

- status code
- response length
- response content

One IP address will respond differently, indicating the location of the internal admin panel.

---

## Discovering the Admin Panel

The scan reveals an internal admin interface:

```
http://192.168.0.218:8080/admin
```

Accessing this endpoint through the SSRF vulnerability displays the admin page.

---

## Deleting the Target User

The admin panel contains functionality to delete users.

Trigger the delete action using the SSRF parameter:

```
stockApi=http://192.168.0.218:8080/admin/delete?username=carlos
```

Because the request is executed by the server, it successfully deletes the user.

Once the user **carlos** is deleted, the lab is solved.

---

## Tools Used

- Burp Suite
- Burp Intruder
- PortSwigger Web Security Academy

---

## Key Takeaway

This lab shows how SSRF vulnerabilities can allow attackers to:

- access internal systems
- scan internal networks
- interact with administrative services
- perform unauthorized actions

Even when internal services are not exposed to the internet, SSRF can be used to reach them through the vulnerable server.
