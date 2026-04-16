---
layout: note
title: Active Directory Basics
permalink: /notes/active-directory-basics/
---

# Active Directory Basics

Active Directory (AD) is a directory service created by Microsoft used to manage users, computers, and resources in a network.

It is one of the most common targets in real-world attacks and one of the most important topics in cybersecurity.

## Why Active Directory Matters

Most enterprise environments use Active Directory.

Understanding AD is critical for:
- pentesting internal networks
- red team engagements
- blue team detection and defense
- understanding how organizations manage access

## Key Concepts

### Domain
A domain is a logical group of network objects (users, computers, groups) managed by Active Directory.

### Domain Controller (DC)
A domain controller is the server that runs Active Directory and handles authentication and authorization for the domain.

### Objects
Everything in AD is an object:
- Users
- Computers
- Groups
- Organizational Units (OUs)

### Organizational Unit (OU)
An OU is a container used to organize objects inside a domain.

### Group Policy (GPO)
Group Policy Objects are rules and settings applied to users or computers in a domain.

Examples:
- password policy
- software restrictions
- login scripts

### Trust
A trust is a relationship between two domains that allows users in one domain to access resources in another.

## Authentication in AD

### Kerberos
Kerberos is the default authentication protocol in Active Directory.

Key components:
- KDC (Key Distribution Center) — runs on the domain controller
- TGT (Ticket Granting Ticket) — proves the user is authenticated
- Service Ticket — allows access to a specific service

### NTLM
NTLM is an older authentication protocol still sometimes used as a fallback.

It is less secure than Kerberos and is a common target in attacks.

## Common AD Attack Concepts

For educational understanding in lab environments:

- Kerberoasting — requesting service tickets and cracking them offline
- AS-REP Roasting — targeting accounts that do not require pre-authentication
- Pass-the-Hash — using a password hash instead of the plaintext password
- Pass-the-Ticket — using a stolen Kerberos ticket
- DCSync — simulating domain controller replication to extract credentials
- Golden Ticket — forging a TGT using the krbtgt hash
- Silver Ticket — forging a service ticket

## Common Tools Used in AD Labs

- BloodHound — maps AD relationships and attack paths
- Impacket — Python tools for AD interaction
- Mimikatz — credential extraction tool (lab use only)
- Rubeus — Kerberos interaction tool
- PowerView — PowerShell AD enumeration
- ldapsearch — LDAP query tool
- CrackMapExec — network enumeration and attack tool

## What Blue Teams Watch For

- unusual authentication patterns
- service ticket requests from unexpected users
- DCSync-like replication requests
- new admin accounts
- lateral movement across systems
- Kerberos anomalies

## Good Learning Approach

- start with understanding how AD works normally
- learn authentication flow before studying attacks
- practice in authorized lab environments like TryHackMe or Hack The Box
- learn both the attack and the detection side
- take detailed notes on each concept

## Final Note

Active Directory is not just a pentesting topic.

It is a critical part of how organizations operate, and understanding it helps in offense, defense, and security analysis.
