---
layout: default
title: Roadmap
---

# Roadmap

A step-by-step learning path from zero to advanced cybersecurity topics.  
Follow the phases in order. Each phase builds on the last.

---

## Phase 1 — Foundations
> Start here. No experience needed.

Build your base before touching any tools.

- [Networking Basics]({{ site.baseurl }}/notes/networking-basics/) — IP, TCP/UDP, DNS, ports, how the internet works
- [Linux for Security]({{ site.baseurl }}/notes/linux-for-security/) — commands, file system, permissions, bash basics
- [Security Analyst Basics]({{ site.baseurl }}/notes/security-analyst-basics/) — core concepts, CIA triad, threats, terminology

✅ When you finish Phase 1 you should be comfortable in a Linux terminal and understand how networks communicate.

---

## Phase 2 — Recon and Web Skills
> Learn how to find things and how the web works under the hood.

- [Enumeration Basics]({{ site.baseurl }}/notes/enumeration-basics/) — scanning, banner grabbing, finding attack surfaces
- [Nmap Basics]({{ site.baseurl }}/notes/nmap-basics/) — port scanning, service detection, NSE scripts
- [Web Application Testing Basics]({{ site.baseurl }}/notes/web-application-testing-basics/) — HTTP, requests, responses, how web apps work
- [Burp Suite Basics]({{ site.baseurl }}/notes/burp-suite-basics/) — intercepting traffic, repeater, intruder
- [OSINT Basics]({{ site.baseurl }}/notes/osint-basics/) — finding information from public sources

✅ When you finish Phase 2 you should be able to scan a target, browse its traffic in Burp Suite, and gather open-source intelligence.

---

## Phase 3 — Attack Techniques
> Learn how attacks work so you can test and defend against them.

- [Authentication and Sessions]({{ site.baseurl }}/notes/authentication-and-sessions/) — cookies, tokens, session hijacking, broken auth
- [SQL Injection Basics]({{ site.baseurl }}/notes/sql-injection-basics/) — finding and exploiting SQLi, tools, mitigations
- [XSS Basics]({{ site.baseurl }}/notes/xss-basics/) — reflected, stored, DOM-based XSS, payloads, mitigations
- [Password Attacks Basics]({{ site.baseurl }}/notes/password-attacks-basics/) — wordlists, Hydra, John, Hashcat, hash cracking
- [Metasploit Basics]({{ site.baseurl }}/notes/metasploit-basics/) — framework overview, exploits, payloads, Meterpreter

✅ When you finish Phase 3 you should be able to identify and manually test common web vulnerabilities and use standard attack tools in a lab.

---

## Phase 4 — Blue Team and Detection
> Learn how defenders think, monitor, and respond.

- [Log Analysis Basics]({{ site.baseurl }}/notes/log-analysis-basics/) — reading system and application logs
- [SIEM Basics]({{ site.baseurl }}/notes/siem-basics/) — what a SIEM is, log ingestion, alert rules
- [Incident Response Basics]({{ site.baseurl }}/notes/incident-response-basics/) — IR lifecycle, triage, containment, reporting

✅ When you finish Phase 4 you should understand how defenders detect and respond to the attacks from Phase 3.

---

## Phase 5 — Advanced Topics
> Harder concepts. Requires everything before this.

- [Privilege Escalation Intro]({{ site.baseurl }}/notes/privilege-escalation-intro/) — Linux and Windows privesc concepts
- [Active Directory Basics]({{ site.baseurl }}/notes/active-directory-basics/) — AD structure, users, groups, common attacks
- [Red Teaming vs Pentesting]({{ site.baseurl }}/notes/red-teaming-vs-pentesting/) — methodology, differences, workflow
- [CTF Tips for Beginners]({{ site.baseurl }}/notes/ctf-tips/) — categories, tools, mindset, practice platforms

✅ When you finish Phase 5 you have a strong all-round foundation in both offensive and defensive security.

---

## Coming Soon — Future Plans

These topics are planned and will be added to the hub:

**Attack and Exploitation**
- File Inclusion (LFI / RFI)
- Command Injection
- XXE (XML External Entity)
- SSRF (Server-Side Request Forgery)
- CSRF Basics
- Buffer Overflow Intro
- Windows Privilege Escalation

**Tools and Workflow**
- Gobuster and Directory Brute Forcing
- Nikto Basics
- Netcat and Socat
- Wireshark Basics
- CyberChef Guide

**Blue Team and Forensics**
- Memory Forensics Intro
- Disk Forensics Basics
- Malware Analysis Intro
- Threat Hunting Basics
- Detection Engineering Basics

**Active Directory (Advanced)**
- Kerberoasting
- Pass-the-Hash
- BloodHound and AD Enumeration
- Domain Privilege Escalation

**Career and Certification**
- CompTIA Security+ Study Notes
- eJPT Prep Guide
- TryHackMe Learning Path Guide
- Building a Home Lab
- Writing a Security Report

---

## Suggested Order for Complete Beginners

If you have never studied cybersecurity before, follow this exact sequence:

1. Networking Basics
2. Linux for Security
3. Security Analyst Basics
4. Enumeration Basics
5. Nmap Basics
6. Web Application Testing Basics
7. Burp Suite Basics
8. OSINT Basics
9. Authentication and Sessions
10. SQL Injection Basics
11. XSS Basics
12. Password Attacks Basics
13. Log Analysis Basics
14. SIEM Basics
15. Incident Response Basics
16. Metasploit Basics
17. Privilege Escalation Intro
18. Active Directory Basics
19. Red Teaming vs Pentesting
20. CTF Tips for Beginners
