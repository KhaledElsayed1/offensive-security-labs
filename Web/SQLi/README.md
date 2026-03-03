# SQL Injection (SQLi)

## Overview

SQL Injection (SQLi) is a critical web security vulnerability that allows attackers to interfere with database queries executed by an application.

It occurs when user input is directly included in SQL statements without proper sanitization or parameterization.

- **OWASP Top 10:** A03 – Injection  
- **CWE-89:** Improper Neutralization of Special Elements used in an SQL Command  

---

## What is SQL Injection?

When an application dynamically builds SQL queries using unsanitized user input, an attacker can manipulate the query logic.

Example vulnerable pattern:

```sql
SELECT * FROM users WHERE username = 'USER_INPUT';
