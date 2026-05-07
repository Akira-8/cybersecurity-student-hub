---
layout: default
title: IDOR (Insecure Direct Object Reference)
---

# IDOR — Insecure Direct Object Reference

## What is IDOR

IDOR occurs when an application uses a user-controllable value to directly access objects — files, database records, accounts — without checking whether the user is authorised to access that specific object.

It is one of the most common and impactful vulnerabilities found in bug bounty programmes.

---

## Simple Example

You view your own profile:
https://example.com/profile?id=1001

You change the ID to someone else's:
https://example.com/profile?id=1002

If you can see another user's profile data, that is an IDOR.

---

## Where to Find IDORs

Look for any reference to an object that you control in a request:

| Location | Example |
|----------|---------|
| URL parameter | `?id=123`, `?user=456`, `?order=789` |
| URL path | `/api/users/123/profile` |
| POST body | `{"user_id": 123, "action": "delete"}` |
| Cookie | `user_id=123` in a cookie value |
| HTTP header | `X-User-ID: 123` |
| JSON API response | IDs returned in responses you can then reference |
| File names | `/invoices/invoice-1234.pdf` |

---

## Types of IDOR

### Horizontal privilege escalation

Accessing another user's data at the same privilege level.
/api/messages?user_id=1001   →   change to user_id=1002

User 1001 reads user 1002's private messages.

### Vertical privilege escalation

Accessing resources belonging to a higher privilege level.
/api/admin/users?id=1001

A normal user accesses an admin endpoint.

### IDOR on actions

Not just reading — performing actions on objects you do not own:
POST /api/orders/delete
{"order_id": 9876}

Deleting someone else's order.

---

## IDOR with Non-Numeric IDs

Not all IDORs use sequential integers. Look for:

**GUIDs/UUIDs:**
/api/documents/a3f2c1d4-e5b6-7890-abcd-ef1234567890
If GUIDs are predictable or leaked in other responses, they can still be vulnerable.

**Hashed IDs:**
/files/5f4dcc3b5aa765d61d8327de.pdf
If it is an MD5 of a filename or ID, you can generate your own hashes.

**Base64 encoded values:**
/profile?id=dXNlcl8xMDAx
Decode: `user_1001` → change to `user_1002` → encode back.

---

## Finding Hidden IDORs

### Check API calls in Burp Suite

Many IDORs are in API calls that are not visible in the browser UI. Intercept all traffic and look through the HTTP history in Burp.

### Swap IDs between accounts

Set up two test accounts. Log in as Account A, perform actions, capture requests. Replace Account A's IDs with Account B's IDs. Send requests while authenticated as Account A.

### Look in responses

Sometimes the application returns object IDs in responses that you can then use in other requests.

### Check download and export functions

Document downloads, invoice PDFs, and export features are a goldmine for IDOR.
/download?file=invoice_1234.pdf
/export?report_id=567

---

## IDOR Testing Methodology

1. Map all functionality while logged in — capture every request in Burp
2. Identify every parameter that references an object (ID, name, file, token)
3. Create a second account
4. For each parameter, try:
   - Using Account B's object IDs while authenticated as Account A
   - Incrementing or decrementing numeric IDs
   - Substituting your own IDs into other users' requests
5. Check if the response contains data belonging to a different user
6. Test on all HTTP methods — GET, POST, PUT, DELETE, PATCH

---

## Impact

| Action | Impact |
|--------|--------|
| Read another user's data | Privacy breach, data leak |
| Edit another user's data | Account manipulation |
| Delete another user's data | Data loss, service disruption |
| Access admin functions | Full application compromise |
| Access payment / order data | Financial data exposure |

IDOR reports have paid out some of the largest bug bounty rewards.

---

## Tools

- **Burp Suite** — essential for capturing and replaying requests
- **Burp Intruder** — automate ID fuzzing across a range
- **Autorize (Burp extension)** — automatically tests for IDOR and broken access control by replaying requests with a lower-privileged session

### Autorize workflow

1. Install Autorize from Burp BApp Store
2. Copy your lower-privileged user's cookie into Autorize
3. Browse the application as a high-privileged user
4. Autorize replays every request with the low-privileged cookie
5. Flags requests where the response is similar — potential IDOR

---

## Mitigations

- Implement server-side authorisation checks on every request — never trust client-supplied IDs alone
- Use indirect references — map user-specific tokens to actual database IDs server-side
- Validate that the authenticated user owns or has permission to access the requested object
- Use UUIDs instead of sequential integers — but do not rely on this as the only protection
- Log and alert on access to objects by users who do not own them

---

## Practice Labs

- PortSwigger Web Academy: Access control labs (free)
- TryHackMe: IDOR room
- PentesterLab: IDOR exercises
- Bug bounty programmes — IDOR is one of the most commonly reported vulnerabilities

---

## Key Terms

| Term | Meaning |
|------|---------|
| IDOR | Insecure Direct Object Reference |
| Horizontal escalation | Accessing another user's data at the same level |
| Vertical escalation | Accessing higher-privileged resources |
| GUID / UUID | Globally unique identifier — not always safe |
| Access control | Rules defining who can access what |
| Autorize | Burp extension for automated IDOR testing |
| Object reference | Any value pointing to a resource — ID, filename, token |
