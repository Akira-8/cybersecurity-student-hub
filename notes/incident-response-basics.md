---
layout: note
title: Incident Response Basics
permalink: /notes/incident-response-basics/
---

# Incident Response Basics

Incident response (IR) is the process of detecting, investigating, containing, and recovering from security incidents.

It is a core skill for security analysts and blue team professionals.

## What Is a Security Incident?

A security incident is any event that threatens the confidentiality, integrity, or availability of systems or data.

Examples:
- malware infection
- unauthorized access
- data breach
- phishing compromise
- ransomware
- insider threat activity

## The Incident Response Lifecycle

A widely used framework comes from NIST (SP 800-61):

### 1. Preparation
- establish an IR plan
- define roles and responsibilities
- set up tools and monitoring
- conduct training and awareness

### 2. Detection and Analysis
- identify potential incidents through alerts, logs, and reports
- validate whether the activity is a real incident
- determine scope and severity
- collect and preserve evidence

### 3. Containment, Eradication, and Recovery
- contain the threat to prevent further damage
- remove the root cause
- restore affected systems
- verify systems are clean before returning to production

### 4. Post-Incident Activity
- document what happened
- identify lessons learned
- improve detection and response processes
- update the IR plan

## Key Concepts

### Triage
Triage is the process of quickly assessing and prioritizing incidents.

Questions to ask:
- How severe is this?
- How many systems are affected?
- Is data at risk?
- Is the threat still active?

### Indicators of Compromise (IOCs)
IOCs are artifacts that suggest a system has been compromised.

Examples:
- malicious IP addresses
- suspicious file hashes
- unusual domain lookups
- unexpected processes

### Chain of Custody
Chain of custody tracks who handled evidence and when.

This is important for maintaining evidence integrity.

### Containment Strategies
- isolate the affected system from the network
- disable compromised user accounts
- block malicious IPs or domains
- preserve evidence before making changes

## Common IR Tools

- SIEM platforms (Splunk, Elastic, Sentinel)
- EDR solutions (endpoint detection and response)
- Volatility (memory forensics)
- Wireshark (network analysis)
- CyberChef (data decoding)
- VirusTotal (indicator checking)
- TheHive (IR case management)

## Common Mistakes in IR

- not documenting actions taken
- destroying evidence by acting too fast
- failing to contain before investigating
- not communicating with the team
- assuming the incident is over too early

## Final Note

Incident response is about staying calm, following a process, and making decisions based on evidence.

A good responder asks the right questions, preserves evidence, and documents everything clearly.
