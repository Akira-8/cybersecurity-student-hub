---
layout: page
title: Enumeration Basics
permalink: /notes/enumeration-basics/
---

# Enumeration Basics

Enumeration is one of the most important parts of cybersecurity work, especially in pentesting and red teaming.

It is the process of gathering useful information about a target system, service, application, or environment.

## Why Enumeration Matters

Good enumeration helps answer questions like:

- What services are running?
- Which ports are open?
- What technologies are being used?
- Are there directories, users, shares, or endpoints exposed?
- Is there anything misconfigured?

A lot of successful security work comes from strong enumeration.

## Common Areas of Enumeration

### Network Enumeration
This includes identifying:

- live hosts
- open ports
- services
- service versions
- operating system clues

### Web Enumeration
This includes looking for:

- hidden directories
- login pages
- admin panels
- technologies
- API endpoints
- exposed files

### User and Service Enumeration
This may include:

- usernames
- groups
- SMB shares
- DNS records
- email patterns
- system information

## Passive vs Active Enumeration

### Passive Enumeration
Information is collected without directly interacting much with the target.

Examples:
- public websites
- DNS information
- metadata
- public code repositories
- leaked credentials from legal/public sources

### Active Enumeration
Information is collected by interacting directly with the target.

Examples:
- port scanning
- service probing
- web requests
- directory brute forcing in legal lab environments

## Basic Enumeration Workflow

A simple workflow can look like this:

1. identify the target
2. check if the host is alive
3. scan open ports
4. identify running services
5. check versions and technologies
6. enumerate the web application if one exists
7. look for weak points, exposures, or attack surface

## Common Tools Used in Enumeration

- Nmap
- Gobuster
- FFUF
- WhatWeb
- Nikto
- Enum4linux
- Dig
- Whois

## Good Habits During Enumeration

- take notes
- organize findings clearly
- do not rush
- verify results
- separate assumptions from confirmed facts
- stay within legal and authorized scope

## Example Things to Record

When enumerating, useful notes may include:

- IP address
- domain name
- open ports
- detected services
- software versions
- web technologies
- interesting paths
- usernames
- possible attack surface

## Final Note

Enumeration is not just a first step.  
It is a continuous process and often the difference between missing and finding useful opportunities during assessment.
