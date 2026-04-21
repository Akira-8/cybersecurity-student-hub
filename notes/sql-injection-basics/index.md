---
layout: default
title: SQL Injection Basics
---

# SQL Injection Basics

## What is SQL Injection
SQL injection (SQLi) occurs when user input is inserted directly into a SQL query without proper sanitization.

## Why it matters
It is one of the most common and dangerous web vulnerabilities. It can lead to data theft, authentication bypass, and full database compromise.

## Types of SQLi

- **In-band SQLi** – results returned directly in the response
  - Error-based: extracts data through error messages
  - Union-based: uses UNION to retrieve data from other tables
- **Blind SQLi** – no visible output; you infer from behavior
  - Boolean-based: true/false conditions change the response
  - Time-based: uses SLEEP() or similar to detect injection
- **Out-of-band SQLi** – uses DNS or HTTP requests to exfiltrate data

## Basic Example

Vulnerable query:
```sql
SELECT * FROM users WHERE username = '$input';
```

Injection:
' OR '1'='1

Resulting query:
```sql
SELECT * FROM users WHERE username = '' OR '1'='1';
```

## Auth Bypass Example
Username: admin'--
Password: anything

This comments out the rest of the query.

## UNION-Based Example
```sql
' UNION SELECT null, username, password FROM users--
```

## How to Test (Ethically, on your own lab)
1. Find input fields, URL parameters, cookies
2. Try `'` to see if an error occurs
3. Try `' OR '1'='1` to test boolean bypass
4. Use Burp Suite to intercept and modify requests

## Tools
- **sqlmap** – automated SQLi detection and exploitation
- **Burp Suite** – manual testing and interception

## Mitigations
- Use prepared statements / parameterized queries
- Input validation and sanitization
- Principle of least privilege on DB accounts
- WAF (Web Application Firewall)

## Practice Labs
- TryHackMe: SQL Injection room
- PortSwigger Web Academy: SQL Injection labs (free)

## Key Terms
- SQLi: SQL Injection
- Payload: the injected string
- Blind injection: no visible output
- OOB: out-of-band
