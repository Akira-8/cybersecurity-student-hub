---
layout: note
title: Log Analysis Basics 
permalink: /notes/log-analysis-basics/
---

# Log Analysis Basics

Log analysis is an important skill for security analysts and blue team learners.

Logs help us understand what happened on a system, network, application, or user account.

## What Is a Log?

A log is a record of an event or action.

Examples:
- a user logging in
- a firewall blocking traffic
- a web server receiving a request
- an endpoint detecting suspicious activity

## Why Log Analysis Matters

Logs help security teams:
- detect attacks
- investigate incidents
- understand timelines
- identify suspicious behavior
- confirm whether an alert is real

## Common Log Sources

### Authentication Logs
These show login activity.

Examples:
- successful logins
- failed logins
- password changes
- account lockouts

### Web Server Logs
These show activity on websites and applications.

Examples:
- page requests
- error codes
- unusual paths
- suspicious user agents

### Firewall Logs
These show allowed or blocked network traffic.

Examples:
- source IP
- destination IP
- ports
- protocol used

### Endpoint Logs
These show activity on devices and hosts.

Examples:
- process creation
- file changes
- registry changes
- suspicious script execution

### DNS Logs
These show domain lookup activity.

Examples:
- queried domain
- query time
- source host
- suspicious or unusual domains

## What to Look For

When reviewing logs, look for:
- repeated failed logins
- unusual login times
- strange IP addresses
- access to unusual files or pages
- unexpected privilege changes
- process activity that does not match normal behavior
- large amounts of requests in a short time

## Basic Investigation Questions

Ask:
- What happened?
- When did it happen?
- Who is involved?
- What system is affected?
- Is this normal or unusual?
- What happened before and after?
- Is there evidence of malicious behavior?

## Simple Workflow

A basic log analysis workflow can be:

1. identify the alert or event
2. find the related logs
3. check the timestamp
4. understand the source and destination
5. compare with normal behavior
6. look for related events
7. decide whether it is benign, suspicious, or malicious
8. document the result

## Common Tools

- SIEM platforms
- Splunk
- Elastic / ELK
- Windows Event Viewer
- Sysmon
- grep
- PowerShell
- CyberChef

## Good Habits

- keep notes in timeline order
- do not rely on one log alone
- check context before deciding
- look for patterns, not just single events
- document everything clearly

## Example Signs of Suspicious Activity

- many failed logins followed by a success
- login from an unusual country or location
- new admin account creation
- strange PowerShell activity
- connections to unknown domains
- unexpected file downloads or script execution

## Final Note

Log analysis is about understanding behavior.

A good analyst can turn raw logs into a story of what happened, when it happened, and whether it matters.
