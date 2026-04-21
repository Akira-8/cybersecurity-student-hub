---
layout: default
title: Roadmap
---

# Roadmap

A step-by-step learning path from zero to advanced cybersecurity.  
Follow the phases in order. Each phase builds on the last.  
New notes are added regularly — check back often.

---

## Phase 1 — Foundations
> Start here. No experience needed.

Build your base before touching any tools. If you skip this, everything else will be harder.

- [Networking Basics]({{ site.baseurl }}/notes/networking-basics/) — IP, TCP/UDP, DNS, ports, OSI model, how the internet works
- [Linux for Security]({{ site.baseurl }}/notes/linux-for-security/) — terminal commands, file system, permissions, bash basics
- [Security Analyst Basics]({{ site.baseurl }}/notes/security-analyst-basics/) — CIA triad, threats, vulnerabilities, core security terminology

**When you finish Phase 1** you should be comfortable in a Linux terminal and understand how networks communicate.

---

## Phase 2 — Recon and Enumeration
> Learn how to find things before you attack anything.

- [Enumeration Basics]({{ site.baseurl }}/notes/enumeration-basics/) — scanning methodology, banner grabbing, attack surface mapping
- [Nmap Basics]({{ site.baseurl }}/notes/nmap-basics/) — port scanning, service and OS detection, NSE scripts, output formats
- [OSINT Basics]({{ site.baseurl }}/notes/osint-basics/) — finding information from public sources, Google dorking, tools

**When you finish Phase 2** you should be able to scan a target network and gather open-source intelligence on a target.

---

## Phase 3 — Web Application Security
> Understand how the web works and how it breaks.

- [Web Application Testing Basics]({{ site.baseurl }}/notes/web-application-testing-basics/) — HTTP, requests, responses, cookies, how web apps work
- [Burp Suite Basics]({{ site.baseurl }}/notes/burp-suite-basics/) — intercepting traffic, repeater, intruder, decoder
- [Authentication and Sessions]({{ site.baseurl }}/notes/authentication-and-sessions/) — cookies, tokens, session hijacking, broken authentication
- [SQL Injection Basics]({{ site.baseurl }}/notes/sql-injection-basics/) — in-band, blind, union-based SQLi, sqlmap, mitigations
- [XSS Basics]({{ site.baseurl }}/notes/xss-basics/) — reflected, stored, DOM-based XSS, payloads, CSP, mitigations

**When you finish Phase 3** you should be able to identify and manually test the most common web vulnerabilities using Burp Suite.

---

## Phase 4 — Attack Tools and Techniques
> Learn the tools used in real engagements.

- [Password Attacks Basics]({{ site.baseurl }}/notes/password-attacks-basics/) — wordlists, Hydra, John the Ripper, Hashcat, hash cracking, spraying
- [Metasploit Basics]({{ site.baseurl }}/notes/metasploit-basics/) — framework overview, modules, exploits, payloads, Meterpreter, msfvenom

**When you finish Phase 4** you should be able to run common attack tools in a controlled lab environment.

---

## Phase 5 — Blue Team and Detection
> Learn how defenders think, monitor, and respond.

- [Log Analysis Basics]({{ site.baseurl }}/notes/log-analysis-basics/) — reading system, auth, and application logs, finding suspicious activity
- [SIEM Basics]({{ site.baseurl }}/notes/siem-basics/) — what a SIEM does, log ingestion, correlation rules, alert triage
- [Incident Response Basics]({{ site.baseurl }}/notes/incident-response-basics/) — IR lifecycle, preparation, detection, containment, eradication, reporting

**When you finish Phase 5** you will understand how defenders detect and respond to the attacks covered in Phases 3 and 4.

---

## Phase 6 — Advanced Offensive Topics
> Harder concepts. Requires everything before this.

- [Privilege Escalation Intro]({{ site.baseurl }}/notes/privilege-escalation-intro/) — Linux and Windows privesc concepts, common misconfigurations
- [Active Directory Basics]({{ site.baseurl }}/notes/active-directory-basics/) — AD structure, users, groups, GPO, common attacks
- [Red Teaming vs Pentesting]({{ site.baseurl }}/notes/red-teaming-vs-pentesting/) — methodology, differences, engagements, reporting
- [CTF Tips for Beginners]({{ site.baseurl }}/notes/ctf-tips/) — categories, tools, mindset, platforms, common mistakes

**When you finish Phase 6** you have a strong all-round foundation in both offensive and defensive security and are ready for certifications or deeper specialization.

---

## Suggested Order for Complete Beginners

Follow this exact sequence if you have never studied cybersecurity before:

1. Networking Basics
2. Linux for Security
3. Security Analyst Basics
4. Enumeration Basics
5. Nmap Basics
6. OSINT Basics
7. Web Application Testing Basics
8. Burp Suite Basics
9. Authentication and Sessions
10. SQL Injection Basics
11. XSS Basics
12. Password Attacks Basics
13. Metasploit Basics
14. Log Analysis Basics
15. SIEM Basics
16. Incident Response Basics
17. Privilege Escalation Intro
18. Active Directory Basics
19. Red Teaming vs Pentesting
20. CTF Tips for Beginners

---

## Coming Soon — What We Are Adding Next

These notes are being written and will be published to this hub.

### Web Vulnerabilities
- File Inclusion — LFI and RFI explained with examples
- Command Injection — how it works, blind vs reflected, bypasses
- SSRF — Server-Side Request Forgery, what it can reach
- CSRF — Cross-Site Request Forgery and token bypass
- XXE — XML External Entity injection
- IDOR — Insecure Direct Object References
- Open Redirect — detection and impact

### Tools and Workflow
- Gobuster — directory and DNS brute forcing
- Nikto — web server scanning basics
- Netcat and Socat — listeners, shells, file transfer
- Wireshark Basics — reading pcap files, filtering traffic
- CyberChef Guide — encoding, decoding, chaining operations
- ffuf — fast web fuzzer for directories and parameters

### Active Directory (Advanced)
- Kerberoasting — how it works and how to crack tickets
- Pass-the-Hash — lateral movement with stolen NTLM hashes
- BloodHound — AD enumeration and attack path visualization
- AS-REP Roasting — targeting accounts without pre-auth
- Domain Privilege Escalation paths

### Windows Security
- Windows Privilege Escalation — common techniques and tools
- Windows Persistence Basics — registry, services, scheduled tasks
- PowerShell for Security — recon and attack scripts

### Forensics and Blue Team (Advanced)
- Memory Forensics Intro — Volatility basics, process analysis
- Disk Forensics Basics — artifacts, timeline analysis
- Malware Analysis Intro — static and dynamic analysis
- Threat Hunting Basics — hypothesis-driven hunting
- Detection Engineering Basics — writing detection rules

### Career and Certifications
- CompTIA Security+ Study Notes
- eJPT Exam Prep Guide
- TryHackMe Learning Path Guide
- Building a Home Lab — VMs, networking, vulnerable machines
- Writing a Pentest Report — structure, findings, severity ratings
- Bug Bounty Basics — how to start, platforms, methodology

---

## How This Hub Grows

Notes are added based on:
- what the community asks for in [Discussions](https://github.com/akira-8/cybersecurity-student-hub/discussions)
- what topics come up on TryHackMe and real learning paths
- what is most useful for students going into security analyst or pentesting roles

If you want a topic added, open a discussion or suggest it in the repo.
