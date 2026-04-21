---
layout: default
title: Password Attacks Basics
---

# Password Attacks Basics

## Overview
Password attacks are techniques used to recover or crack passwords. Understanding them helps defenders build stronger authentication.

## Types of Password Attacks

### Brute Force
Try every possible combination until correct.
- Very slow for long passwords
- Effective against short or simple passwords

### Dictionary Attack
Try passwords from a wordlist.
- Much faster than pure brute force
- Effective against common passwords

### Credential Stuffing
Use leaked username/password pairs from other breaches.
- Works when users reuse passwords
- Large-scale automated attacks

### Password Spraying
Try one common password against many accounts.
- Avoids lockouts by not hammering one account
- Effective in Active Directory environments

### Hash Cracking
Recover plaintext from a password hash.
- Offline attack on stolen hash database
- Faster than online attacks

## Common Wordlists
- **rockyou.txt** – most common wordlist, 14M passwords
- **SecLists** – collection of wordlists for many purposes
- Custom wordlists from OSINT on the target

## Tools

### Hydra (online brute force)
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.1
hydra -l admin -P rockyou.txt 192.168.1.1 http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
```

### John the Ripper (hash cracking)
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --format=bcrypt --wordlist=rockyou.txt hashes.txt
```

### Hashcat (GPU-based hash cracking)
```bash
hashcat -m 0 hashes.txt rockyou.txt        # MD5
hashcat -m 1000 hashes.txt rockyou.txt     # NTLM
hashcat -m 3200 hashes.txt rockyou.txt     # bcrypt
```

## Hash Identification
Use `hash-identifier` or check hash length and format:
| Hash | Length | Example start |
|------|--------|---------------|
| MD5  | 32 chars | 5f4dcc... |
| SHA1 | 40 chars | — |
| SHA256 | 64 chars | — |
| NTLM | 32 chars | — |
| bcrypt | 60 chars | $2b$ |

## Mitigations
- Use long, random passwords (12+ chars)
- Multi-factor authentication (MFA)
- Account lockout policies
- Password managers
- Don't reuse passwords across sites
- Store passwords with bcrypt, scrypt, or Argon2 (not MD5 or SHA1)

## Practice Labs
- TryHackMe: John the Ripper, Hydra rooms
- Crack the Hash challenge on TryHackMe

## Key Terms
- Hash: one-way function output from a password
- Salt: random value added to a password before hashing
- Rainbow table: precomputed hash lookup table
- Offline attack: attacking a hash without hitting the live service
