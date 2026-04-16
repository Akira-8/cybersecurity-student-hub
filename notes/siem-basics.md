---
layout: note
title: SIEM Basics
permalink: /notes/siem-basics/
---

# SIEM Basics

SIEM stands for Security Information and Event Management.

It is one of the most important tools used by security analysts to detect, investigate, and respond to security events.

## What a SIEM Does

A SIEM platform:
- collects logs from many sources
- normalizes and stores log data
- correlates events across systems
- generates alerts based on rules or patterns
- provides a search interface for investigation
- supports dashboards and reporting

## Why SIEM Matters

Without a SIEM, security teams would have to check logs manually on every system.

A SIEM centralizes all that data and helps analysts:
- find threats faster
- see patterns across the environment
- investigate incidents with full context
- meet compliance and audit requirements

## Common Log Sources Feeding a SIEM

- firewalls
- web servers
- authentication systems
- endpoint detection tools
- email gateways
- DNS servers
- proxy servers
- cloud services
- operating system event logs

## Key SIEM Concepts

### Event
An event is a single recorded action, like a login attempt or a firewall rule match.

### Alert
An alert is triggered when events match a detection rule or threshold.

Example: 10 failed logins from the same IP in 1 minute.

### Correlation
Correlation links related events across different log sources to identify attack patterns.

Example: a failed login on the VPN followed by a successful login and then data access from an unusual location.

### Dashboard
A dashboard provides a visual overview of security activity, alerts, and trends.

### Query / Search
Analysts use search queries to look through logs for specific events, users, IPs, or indicators.

### Rule
A rule defines what activity should generate an alert.

Rules can be based on:
- thresholds (too many events in a time window)
- specific indicators (known bad IP)
- sequences (event A followed by event B)

## Common SIEM Platforms

- Splunk
- Elastic Security / ELK Stack
- Microsoft Sentinel
- IBM QRadar
- Google Chronicle
- Wazuh

## Basic SIEM Workflow for an Analyst

1. Receive an alert from the SIEM
2. Review the alert details (source, destination, timestamp, rule triggered)
3. Search for related events in the SIEM
4. Check if the activity is expected or suspicious
5. Look for indicators of compromise
6. Determine if the event is benign, suspicious, or malicious
7. Escalate or document findings

## Example SIEM Scenarios

### Brute Force Detection
The SIEM detects 50 failed logins to one account in 2 minutes, followed by a successful login.

### Suspicious Outbound Traffic
The SIEM alerts on a workstation connecting to a known malicious domain repeatedly at 3 AM.

### Lateral Movement
The SIEM correlates a compromised user account being used to authenticate to multiple internal systems in a short time.

## Tips for Learning SIEM

- practice with free tools like Splunk Free or Elastic
- learn basic search queries and filters
- try building simple detection rules
- understand what normal looks like before hunting for abnormal
- focus on understanding the data, not just the tool

## Final Note

A SIEM is powerful, but it is only as good as the data it receives, the rules it uses, and the analyst who investigates its alerts.

Understanding SIEM is essential for anyone pursuing a security analyst or blue team career.
