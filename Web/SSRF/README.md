# Server-Side Request Forgery (SSRF)

## Overview

Server-Side Request Forgery (SSRF) is a web security vulnerability that allows an attacker to cause the server-side application to make HTTP requests to an arbitrary domain or internal resource.

Instead of the attacker directly sending requests to the target system, the vulnerable server performs the request on behalf of the attacker.

This can allow attackers to access internal systems that are normally not reachable from the external network.

---

## How SSRF Works

Many applications fetch remote resources based on user input.

Examples include:

- fetching stock information
- retrieving images
- loading external APIs
- importing files from URLs

If the application does not properly validate the URL provided by the user, an attacker can manipulate the request to target internal services.

Example vulnerable request:

```
POST /check-stock HTTP/1.1

stockApi=http://example.com/api
```

If the application blindly fetches this URL, the attacker can replace it with:

```
http://127.0.0.1/admin
```

or

```
http://192.168.0.10/internal
```

This causes the server to interact with internal resources.

---

## Common SSRF Targets

Attackers commonly target:

### Internal Services

```
127.0.0.1
localhost
192.168.x.x
10.x.x.x
172.16.x.x
```

These addresses may host internal dashboards or administrative panels.

---

### Cloud Metadata Services

In cloud environments such as AWS:

```
http://169.254.169.254/latest/meta-data/
```

This endpoint may expose sensitive information such as:

- access keys
- IAM credentials
- instance metadata

---

### Internal APIs

Internal APIs may allow attackers to:

- access private data
- perform administrative actions
- delete users
- change system configurations

---

## Types of SSRF

### Basic SSRF

The attacker can directly view the response from the internal service.

Example:

```
stockApi=http://127.0.0.1/admin
```

---

### Blind SSRF

The attacker cannot see the response but can trigger requests to external servers.

Used techniques:

- DNS callbacks
- Burp Collaborator
- request timing

---

## Impact

SSRF can lead to severe consequences including:

- internal network scanning
- accessing restricted admin panels
- reading sensitive internal data
- cloud credential theft
- remote command execution in some cases

Because the requests originate from the server, they often bypass firewalls and access controls.

---

## Prevention

To mitigate SSRF vulnerabilities:

- validate and sanitize user-supplied URLs
- use allowlists for trusted domains
- block requests to internal IP ranges
- disable unnecessary outbound requests
- implement network segmentation
- use firewall rules to block internal resource access

---

## References

OWASP SSRF

https://owasp.org/www-community/attacks/Server_Side_Request_Forgery

PortSwigger Web Security Academy

https://portswigger.net/web-security/ssrf
