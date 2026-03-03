# Classic SQL Injection

## Overview

Classic (In-Band) SQL Injection occurs when an attacker is able to inject SQL input and observe the result directly within the application's HTTP response.

This is the most common and straightforward form of SQL Injection.

---

## Testing Objective

The goal during testing was to determine:

- Whether user-controlled input was reflected in database queries
- Whether query logic could be altered
- Whether different responses were returned based on input manipulation

---

## Methodology (High-Level)

During authorized testing:

1. Identified a parameter interacting with the database.
2. Tested how the application handled unexpected input.
3. Observed response behavior differences.
4. Confirmed injection by analyzing application responses.

The vulnerability was confirmed when application behavior changed based on logical query manipulation.

---

## Attack Behavior

Classic SQL Injection allows attackers to:

- Bypass authentication
- Retrieve unintended data
- Manipulate query conditions
- Trigger database errors

Because the results are returned directly in the response, this type of SQLi is often easier to detect.

---

## Impact

If exploited in a real-world scenario, this vulnerability could allow:

- Unauthorized account access
- Exposure of sensitive information
- Modification of stored data
- Administrative function abuse

Severity depends on the affected functionality and database permissions.

---

## Root Cause

The vulnerability existed due to:

- Direct insertion of user input into SQL queries
- Lack of parameterized statements
- No strict input validation
- Insufficient backend protections

---

## Evidence



---

## Mitigation

To prevent Classic SQL Injection:

- Implement parameterized queries
- Validate and sanitize user input
- Avoid dynamic query concatenation
- Limit database privileges
