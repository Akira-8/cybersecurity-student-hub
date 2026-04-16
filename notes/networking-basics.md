---
layout: note
title: Networking Basics
permalink: /notes/networking-basics/
---

# Networking Basics

Networking is one of the most important foundations in cybersecurity.

Almost every attack, defense, and investigation involves understanding how data moves between systems.

## Why Networking Matters in Security

If you do not understand networking, it becomes very difficult to:
- analyze traffic
- understand attack paths
- interpret logs
- use security tools effectively
- investigate incidents

## Key Concepts

### IP Address
An IP address identifies a device on a network.

There are two versions:
- IPv4 (example: 192.168.1.10)
- IPv6 (example: 2001:0db8::1)

### MAC Address
A MAC address is a hardware identifier for a network interface.

It operates at Layer 2 of the OSI model.

### Port
A port is a number used to identify a specific service or application on a device.

Common examples:
- Port 22 — SSH
- Port 80 — HTTP
- Port 443 — HTTPS
- Port 53 — DNS
- Port 445 — SMB
- Port 3389 — RDP

### Protocol
A protocol is a set of rules that defines how data is transmitted.

Common protocols:
- TCP — reliable, connection-based
- UDP — faster, connectionless
- ICMP — used for ping and diagnostics
- HTTP/HTTPS — web traffic
- DNS — domain name resolution
- ARP — maps IP to MAC addresses

## The OSI Model

The OSI model breaks networking into 7 layers:

1. Physical — cables, signals
2. Data Link — MAC addresses, switches
3. Network — IP addresses, routing
4. Transport — TCP, UDP, ports
5. Session — managing connections
6. Presentation — encryption, formatting
7. Application — HTTP, DNS, FTP

For security work, the most commonly referenced layers are 2, 3, 4, and 7.

## The TCP/IP Model

A simpler model used in practice:

1. Network Access — physical + data link
2. Internet — IP, routing
3. Transport — TCP, UDP
4. Application — HTTP, DNS, SSH

## TCP Three-Way Handshake

TCP connections start with a three-way handshake:

1. SYN — client sends a connection request
2. SYN-ACK — server acknowledges and responds
3. ACK — client confirms the connection

This is important to understand for port scanning and traffic analysis.

## DNS

DNS translates domain names to IP addresses.

Example:
- You type example.com
- DNS resolves it to 93.184.216.34

DNS is important in security because attackers often use suspicious or malicious domains.

## DHCP

DHCP automatically assigns IP addresses to devices on a network.

## Subnetting Basics

Subnetting divides a network into smaller segments.

A subnet mask like 255.255.255.0 (/24) means 256 addresses in a subnet.

Understanding subnetting helps with:
- network scanning
- identifying scope
- understanding network layout

## Common Network Devices

- Router — connects networks and routes traffic
- Switch — connects devices within a network
- Firewall — controls traffic based on rules
- Proxy — acts as an intermediary for requests

## Common Network-Based Attacks

- port scanning
- man-in-the-middle
- ARP spoofing
- DNS poisoning
- denial of service
- packet sniffing

## Useful Commands

```bash
ping 192.168.1.1        # test if host is alive
traceroute 8.8.8.8      # trace the path to a host
nslookup example.com    # DNS lookup
dig example.com          # detailed DNS lookup
ifconfig                 # show network interfaces (Linux)
ip a                     # show network interfaces (modern Linux)
netstat -tulnp           # show open ports and connections
ss -tulnp                # modern alternative to netstat
arp -a                   # show ARP table
