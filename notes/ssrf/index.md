---
layout: default
title: SSRF (Server-Side Request Forgery)
---

# SSRF — Server-Side Request Forgery

## What is SSRF

SSRF occurs when an attacker can make the server send HTTP requests to a location of their choosing. The request comes from the server itself, which means it can reach internal systems that are not accessible from the internet.

---

## Why it is Dangerous

Web servers often have access to:
- Internal admin panels not exposed to the internet
- Cloud metadata services (AWS, GCP, Azure)
- Internal APIs and databases
- Other servers on the internal network

An SSRF vulnerability lets an attacker use the server as a proxy to reach all of these.

---

## How it Happens

A web application that fetches a URL on behalf of the user:
https://example.com/fetch?url=https://external-site.com/image.jpg

An attacker changes the URL:
https://example.com/fetch?url=http://localhost/admin

The server fetches its own admin panel and returns the response to the attacker.

---

## What Attackers Target

### Internal admin interfaces
http://localhost/admin
http://127.0.0.1:8080
http://192.168.1.1/admin

### Cloud metadata endpoints

AWS:
http://169.254.169.254/latest/meta-data/
http://169.254.169.254/latest/meta-data/iam/security-credentials/

GCP:
http://metadata.google.internal/computeMetadata/v1/

Azure:
http://169.254.169.254/metadata/instance

These endpoints return cloud credentials, instance roles, and configuration data that can lead to full cloud account takeover.

### Internal port scanning
http://127.0.0.1:22
http://127.0.0.1:3306
http://127.0.0.1:6379

Response differences (size, timing, error messages) reveal which ports are open.

---

## Types of SSRF

### Basic SSRF

Response is returned directly in the HTTP response. You can read the content of internal pages.

### Blind SSRF

No response is returned. You detect it through:
- DNS lookups to a controlled server
- HTTP requests to Burp Collaborator or interactsh
- Timing differences
http://YOUR-COLLABORATOR-URL/test

If your server gets a hit, SSRF is confirmed.

---

## SSRF Bypass Techniques

Applications often try to block `localhost` and `127.0.0.1`. Common bypasses:
http://127.1                  — shortened IP
http://0                      — resolves to localhost on Linux
http://0.0.0.0
http://[::1]                  — IPv6 loopback
http://127.0.0.1.nip.io       — DNS resolves to 127.0.0.1
http://2130706433             — decimal representation of 127.0.0.1
http://0x7f000001             — hex representation of 127.0.0.1

Open redirect chaining:
If the app follows redirects, use an open redirect on a trusted domain
to redirect to 127.0.0.1

URL parser confusion:
http://attacker.com@127.0.0.1/
http://127.0.0.1#attacker.com

---

## SSRF via Common Input Locations

Look for SSRF wherever a URL or hostname appears in user input:

- Document converters (PDF, HTML to image)
- Webhook URL fields
- Image URL import features
- "Check URL" or URL preview functionality
- XML input with external entities
- HTTP header values: `Referer`, `X-Forwarded-For`, `Host`
- API parameters containing URLs

---

## Real-World Impact Examples

- Capital One breach (2019) — SSRF used to hit AWS metadata and steal IAM credentials
- GitLab SSRF — internal Grafana instance accessed
- SSRF is in the OWASP Top 10 (2021) as a standalone category

---

## Tools

- **Burp Suite** — intercept and modify URL parameters
- **Burp Collaborator** — detect blind SSRF via OOB callbacks
- **interactsh** — open-source alternative to Collaborator
- **SSRFmap** — automated SSRF detection and exploitation

---

## Mitigations

- Whitelist allowed URLs, IPs, and domains — deny everything else
- Block requests to private IP ranges: `10.x`, `172.16.x`, `192.168.x`, `127.x`, `169.254.x`
- Disable HTTP redirects or validate redirect destinations
- Do not return raw server responses to users
- Use a dedicated egress proxy that enforces allowlists
- On cloud: use IMDSv2 which requires a session token (not just a GET request)

---

## Practice Labs

- PortSwigger Web Academy: SSRF labs (free, excellent coverage)
- TryHackMe: SSRF room
- HackTheBox machines with internal services

---

## Key Terms

| Term | Meaning |
|------|---------|
| SSRF | Server-Side Request Forgery |
| Metadata endpoint | Cloud service that returns instance credentials |
| Blind SSRF | SSRF where response is not visible |
| OOB | Out-of-band — detecting via DNS/HTTP callbacks |
| IMDS | Instance Metadata Service (AWS, GCP, Azure) |
| IMDSv2 | Improved AWS metadata service requiring session token |
| Egress | Outbound network traffic from the server |
