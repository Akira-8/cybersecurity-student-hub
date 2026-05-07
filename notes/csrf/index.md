---
layout: default
title: CSRF (Cross-Site Request Forgery)
---

# CSRF — Cross-Site Request Forgery

## What is CSRF

CSRF tricks an authenticated user's browser into making unwanted requests to a web application. The application sees the request as legitimate because it comes with the victim's session cookies automatically attached by the browser.

---

## How it Works

1. Victim logs into `bank.com` — browser stores session cookie
2. Victim visits attacker's malicious page
3. Malicious page sends a hidden request to `bank.com/transfer`
4. Browser automatically attaches the session cookie
5. Bank processes the transfer as if the victim requested it

The attacker never sees the response — they just need the action to happen.

---

## Classic Example

The vulnerable request:
```http
POST /transfer HTTP/1.1
Host: bank.com
Cookie: session=abc123

amount=1000&to=attacker-account
```

Attacker's malicious HTML page:
```html

  
    
      
      
    
    document.getElementById('csrfForm').submit();
  

```

When the victim loads this page, the form is submitted silently.

---

## GET-Based CSRF

If a sensitive action uses a GET request:

```html

```

Simply loading the image triggers the request. No user interaction needed.

---

## What CSRF Can Do

- Transfer money
- Change email address or password
- Add an attacker-controlled admin account
- Delete data
- Change security settings

CSRF cannot read responses — it is a one-way attack. Use XSS if you need to read data.

---

## CSRF Tokens

The main defence. A unique, unpredictable token is added to every form and verified server-side.

```html

  
  

```

The attacker cannot know the token, so they cannot construct a valid request.

### Common CSRF token weaknesses

- Token not validated server-side
- Token tied to a different user's session
- Token present but not checked if omitted
- Predictable token (sequential numbers, timestamp-based)
- Token validated but not tied to the user session

---

## Bypassing CSRF Protections

### Remove the token entirely
Some apps only validate the token if it is present. Try removing it completely.

### Use another user's token
Some apps validate the token exists but not that it belongs to the current user.

### Change POST to GET
Some apps apply CSRF protection to POST but not GET.

### Referer header bypass
If protection is based on the Referer header:
Remove the Referer header entirely using:
<meta name="referrer" content="no-referrer">
````
SameSite cookie bypass
SameSite=Lax  — cookies sent on top-level GET navigations
SameSite=None — cookies sent cross-site (requires Secure flag)
If SameSite=Lax, use a GET-based attack via a top-level navigation (window.open or link click).

CSRF vs XSS
CSRFXSSRequires JSNoYesCan read responsesNoYesNeeds victim to be logged inYesNoBypassed by CSRF tokenYesNoUses victim's credentialsYesDepends
XSS can be used to steal CSRF tokens, making it a complete bypass.

Tools

Burp Suite — right-click any request → Engagement tools → Generate CSRF PoC
This generates a ready-to-use HTML page for testing CSRF


Mitigations

Use CSRF tokens on all state-changing requests — validate server-side every time
Set SameSite=Strict or SameSite=Lax on session cookies
Check the Origin and Referer headers as a secondary defence
Use Double Submit Cookie pattern if stateless tokens are needed
Require re-authentication for sensitive actions (password change, payment)


Practice Labs

PortSwigger Web Academy: CSRF labs (free, excellent)
TryHackMe: CSRF room
DVWA: CSRF module


Key Terms
TermMeaningCSRFCross-Site Request ForgeryCSRF tokenUnique secret value tied to a user sessionSameSiteCookie attribute controlling cross-site sendingDouble submit cookieCSRF defence using matching cookie and parameterState-changing requestAny request that modifies data (POST, PUT, DELETE)RefererHTTP header containing the originating page URL
