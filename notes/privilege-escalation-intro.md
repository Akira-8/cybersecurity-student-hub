---
layout: note
title: Privilege Escalation Intro
permalink: /notes/privilege-escalation-intro/
---

# Privilege Escalation Intro

Privilege escalation is the process of gaining higher permissions on a system after initial access has already been achieved in an authorized environment.

It is an important topic in pentesting and red teaming because many attacks become serious only after an attacker gains more permissions.

## What Is Privilege Escalation?

A system usually has different privilege levels.

Examples:
- normal user
- administrator
- root
- service account
- privileged group member

Privilege escalation means moving from a lower level of access to a higher one.

## Why It Matters

If a user or attacker gains more permissions than they should have, they may be able to:

- view sensitive data
- modify system settings
- access restricted files
- control services
- install software
- create new users
- take over the system

## Types of Privilege Escalation

### Vertical Privilege Escalation
This is when a low-privileged user gains access to a higher-privileged account or role.

Example:
- normal user to administrator
- regular user to root

### Horizontal Privilege Escalation
This is when a user accesses another user's data or capabilities with the same level of privilege.

Example:
- one standard user accessing another standard user's account data

## Common Causes

Privilege escalation often happens because of:

- weak file permissions
- misconfigured services
- vulnerable software
- exposed credentials
- insecure scripts
- weak sudo rules
- bad group memberships
- unnecessary admin privileges

## What to Check During Analysis

In a legal lab or assessment, you may look for:

- system permissions
- running services
- scheduled tasks
- environment variables
- user groups
- sudo configuration
- writable files and scripts
- installed software versions
- stored credentials

## Linux Example Areas

On Linux systems, common areas of review include:

- sudo permissions
- SUID/SGID files
- cron jobs
- writable directories
- sensitive configuration files
- shell history
- service files

## Windows Example Areas

On Windows systems, common areas of review include:

- user privileges
- service permissions
- scheduled tasks
- registry settings
- weak file permissions
- local administrator group membership

## Good Learning Mindset

When studying privilege escalation, focus on:

- understanding how permissions work
- identifying misconfigurations
- learning common attack paths
- documenting findings carefully
- staying within authorized lab environments

## Final Note

Privilege escalation is not just about getting higher access.  
It is about understanding how systems are configured and where trust or permission mistakes can create risk.
