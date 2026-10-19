# <img src="./images/network-enumeration-with-nmap.png" width="36" alt="Network Enumeration with Nmap"> Network Enumeration with Nmap

> HTB Academy — Basic Toolset

## Overview

Nmap is a network discovery and security auditing tool used to identify live hosts, open ports, exposed services, and characteristics of authorized target systems.

## Core Concepts

- **Host Discovery:** identifies reachable hosts.
- **Port Scanning:** identifies accessible TCP and UDP ports.
- **Service Enumeration:** identifies services and their versions.
- **OS Detection:** estimates the target operating system.
- **Nmap Scripting Engine (NSE):** extends enumeration through scripts.
- **Output Formats:** saves scan results for analysis and reporting.

## Command Reference

| Objective | Command | Description |
|---|---|---|
| Host discovery | `nmap -sn <target>` | Discovers hosts without a port scan |
| Default scan | `nmap <target>` | Scans common TCP ports |
| Specific ports | `nmap -p 22,80,443 <target>` | Scans selected ports |
| All TCP ports | `nmap -p- <target>` | Scans ports 1–65535 |
| Service detection | `nmap -sV <target>` | Probes detected services |
| Default scripts | `nmap -sC <target>` | Runs default NSE scripts |
| OS detection | `sudo nmap -O <target>` | Attempts operating system detection |
| UDP scan | `sudo nmap -sU --top-ports 100 <target>` | Scans the 100 most common UDP ports |
| Save results | `nmap -oA scan-results <target>` | Saves results in multiple formats |

Replace `<target>` with the authorized lab target. Run scans only against systems you own or have permission to assess.

## Practical Workflow

1. Confirm the authorized target scope.
2. Discover reachable hosts where appropriate.
3. Identify open ports.
4. Enumerate services and versions.
5. Perform additional checks based on the results.
6. Save the output and record relevant findings.

## Lab Notes

Document exercise solutions, observations, and screenshots as the module labs are completed. Store screenshots in `images/` and detailed lab write-ups in `labs/`.

## References

- [Official Nmap Manual](https://nmap.org/book/man.html)
- [Nmap Reference Guide](https://nmap.org/book/)

## Completion

<a href="https://academy.hackthebox.com/achievement/badge/cdfeee8f-972d-11f0-9254-bea50ffe6cb4"><img src="./images/htb-network-enumeration-with-nmap-badge.png" width="120" alt="HTB Academy — The Eye That Sees All Badge"></a>

**Completed:** 21 September 2025
