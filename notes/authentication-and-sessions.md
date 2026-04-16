---
layout: note
title: Authentication and Sessions
permalink: /notes/authentication-and-sessions/
---

# Authentication and Sessions

Authentication and session management are critical concepts in web security.

Many real-world vulnerabilities come from mistakes in how applications verify users and maintain sessions.

## Authentication vs Authorization

### Authentication
Authentication answers: "Who are you?"

It is the process of verifying a user's identity.

Examples:
- username and password
- multi-factor authentication (MFA)
- biometrics
- certificate-based login

### Authorization
Authorization answers: "What are you allowed to do?"

It happens after authentication and controls what resources or actions a user can access.

## Common Authentication Methods

### Username and Password
The most common method. Vulnerable when passwords are weak, reused, or stored insecurely.

### Multi-Factor Authentication (MFA)
MFA requires two or more factors:
- something you know (password)
- something you have (phone, hardware token)
- something you are (fingerprint)

### Token-Based Authentication
A token (like a JWT) is issued after login and sent with each request to prove identity.

### API Keys
API keys authenticate applications rather than individual users.

## Sessions

### What Is a Session?
A session is a way for the server to remember that a user is logged in across multiple requests.

### Session ID
After login, the server creates a session and gives the user a session ID, usually stored in a cookie.

### Session Lifecycle
1. User logs in
2. Server creates a session
3. Session ID is sent to the browser as a cookie
4. Browser sends the session ID with every request
5. Server uses the session ID to identify the user
6. Session ends when the user logs out or the session expires

## Common Vulnerabilities

### Weak Passwords
Applications that allow short or common passwords are easy targets.

### Brute Force
Attackers try many password combinations automatically.

### Credential Stuffing
Attackers use leaked username/password pairs from other breaches.

### Session Hijacking
An attacker steals a valid session ID to impersonate a user.

### Session Fixation
An attacker sets a known session ID before the user logs in, then uses it after authentication.

### Insecure Session Storage
Session IDs stored in URLs or without secure cookie flags can be exposed.

### Missing Logout / Session Expiry
If sessions never expire, stolen tokens remain valid indefinitely.

### Broken Authentication Logic
Logic flaws in login, password reset, or MFA flows that allow bypasses.

## What to Test

- password policy enforcement
- account lockout after failed attempts
- session cookie flags (Secure, HttpOnly, SameSite)
- session expiry behavior
- logout functionality
- MFA bypass possibilities
- password reset flow logic
- token handling and validation

## Good Security Practices

- enforce strong password policies
- implement MFA
- use secure, HttpOnly, SameSite cookie flags
- set session timeouts
- regenerate session IDs after login
- invalidate sessions on logout
- rate limit login attempts
- log authentication events

## Final Note

Authentication and session management are the front door of any application.

If the front door is weak, everything behind it is at risk.
