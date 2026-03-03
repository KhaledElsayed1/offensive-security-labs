# SQL Injection (SQLi)

## Introduction

SQL Injection (SQLi) is a high-impact web application vulnerability that allows an attacker to interfere with the SQL queries an application sends to its database.  
It happens عندما التطبيق يدخل بيانات المستخدم داخل استعلام SQL من غير ما يأمّنها بشكل صحيح (خصوصًا من غير Parameterized Queries).

This vulnerability is classified as:

- **OWASP Top 10:** A03 – Injection  
- **CWE-89:** Improper Neutralization of Special Elements used in an SQL Command  

---

## How SQL Injection Happens

Most web applications interact with a database to:

- authenticate users
- fetch data (products, posts, profiles)
- store data (comments, orders, messages)

When the application builds SQL queries dynamically and merges user input into the query string, the final SQL statement can be altered.

In simple terms:  
**the database executes the final query it receives**, and if user input is not handled safely, the attacker may change the query logic.

---

## Why SQL Injection is Dangerous

Depending on the affected functionality and database permissions, SQL Injection can lead to:

- Authentication bypass
- Sensitive data exposure (users, emails, hashes, tokens)
- Database structure enumeration (tables/columns)
- Data modification or deletion
- Privilege escalation
- In severe cases, full backend compromise (environment dependent)

SQL Injection is typically rated **High to Critical** due to its direct impact on confidentiality and integrity.

---

## Types of SQL Injection

SQLi appears in multiple forms depending on how data is returned and how the application behaves.

### 1) In-Band SQL Injection (Classic)

The attacker can see results directly in the application response.

Common subtypes:

- **Error-Based SQLi:** database errors reveal useful information
- **Union-Based SQLi:** results from another query are merged into the same response

This type is usually the easiest to confirm when responses are verbose.

---

### 2) Blind SQL Injection

The application does not display SQL errors or query results.  
Attackers infer information indirectly.

Common subtypes:

- **Boolean-Based Blind:** differences between TRUE/FALSE responses
- **Time-Based Blind:** delays indicate conditional behavior

Blind SQLi is slower but still very powerful.

---

### 3) Out-of-Band SQL Injection (OOB)

Data is exfiltrated through alternative channels (e.g., DNS/HTTP callbacks).  
This is less common and depends on database/network configuration.

---

## Root Causes

SQL Injection vulnerabilities typically exist due to:

- Building SQL queries using string concatenation
- Missing prepared statements / parameterized queries
- Weak input validation
- Over-privileged database accounts
- Exposing detailed database errors

The core issue is treating user input as trusted SQL code.

---

## Mitigation & Prevention

Recommended defensive measures:

- Use **Parameterized Queries / Prepared Statements**
- Validate input with strict allowlists when possible
- Apply **least privilege** for database users
- Avoid exposing detailed SQL error messages
- Add security testing in CI/CD and perform regular penetration testing

---

## Responsible Disclosure

This repository contains sanitized security documentation created during authorized testing.  
All target identifiers, domains, and sensitive data have been removed.
