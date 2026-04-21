---
layout: default
title: Nmap Basics
---

# Nmap Basics

## What is Nmap
Nmap (Network Mapper) is a free, open-source tool for network discovery and security auditing.

## Why it matters
It is one of the most widely used reconnaissance tools. Understanding Nmap is essential for enumeration and pentesting.

## Basic Syntax
nmap [options] [target]

## Common Scans

### Ping Scan (host discovery)
```bash
nmap -sn 192.168.1.0/24
```

### Default Scan
```bash
nmap 192.168.1.1
```

### Service and Version Detection
```bash
nmap -sV 192.168.1.1
```

### OS Detection
```bash
nmap -O 192.168.1.1
```

### Aggressive Scan (OS + version + scripts + traceroute)
```bash
nmap -A 192.168.1.1
```

### Scan Specific Ports
```bash
nmap -p 22,80,443 192.168.1.1
```

### Scan All 65535 Ports
```bash
nmap -p- 192.168.1.1
```

### UDP Scan
```bash
nmap -sU 192.168.1.1
```

### Stealth SYN Scan
```bash
nmap -sS 192.168.1.1
```

## Scan Types Explained
| Flag | Scan Type | Notes |
|------|-----------|-------|
| -sT | TCP Connect | Full connection, more visible |
| -sS | SYN Stealth | Half-open, less visible |
| -sU | UDP | Slower, often missed |
| -sV | Version | Detects service versions |
| -sC | Default Scripts | Runs NSE scripts |
| -O  | OS Detection | Guesses operating system |

## Output Options
```bash
nmap -oN output.txt target      # normal output
nmap -oX output.xml target      # XML
nmap -oG output.gnmap target    # greppable
nmap -oA output target          # all formats
```

## NSE Scripts
```bash
nmap --script=vuln 192.168.1.1          # run vulnerability scripts
nmap --script=http-title 192.168.1.1    # grab HTTP title
nmap --script=smb-enum-shares target    # SMB enumeration
```

## Key Terms
- NSE: Nmap Scripting Engine
- SYN scan: sends SYN, waits for SYN-ACK, never completes handshake
- Open port: service is listening
- Filtered: firewall blocking the probe

## Practice Labs
- TryHackMe: Nmap room
- Your own local network or a home lab VM
