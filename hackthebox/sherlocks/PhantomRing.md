# PhantomRing — Sherlock (Very Easy)

**Category:** Malware Analysis & Reverse Engineering  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/1296)

## Overview

PhantomRing is a Sherlock challenge focused on static malware analysis and reverse engineering.

The scenario involves a suspicious Linux executable discovered on a system and suspected of making outbound connections. The investigation examines the binary to identify its capabilities, command-and-control (C2) configuration, indicators of compromise (IOCs), and defense-evasion techniques.

## Investigation Focus

- Linux ELF binary triage
- File identification and SHA-256 hashing
- Static analysis of strings, symbols, and executable code
- Command-and-control configuration analysis
- Malware command-handler investigation
- Linux process and session enumeration
- SUID binary discovery routines
- Evasion techniques involving `io_uring`
- eBPF-related security-tool detection
- Linux tracing and anti-forensics behavior
- Self-destruct functionality analysis
- IOC extraction and technical documentation

## Tools and Techniques

- Linux command-line utilities
- `file` and `sha256sum`
- `strings` and `nm`
- `objdump`
- Static binary inspection
- Disassembly and function analysis

## Key Findings

The investigation focused on identifying:

- The binary's architecture and executable format
- Embedded C2 configuration and connection behavior
- Supported commands and their associated capabilities
- System paths used for user and process enumeration
- Routines for discovering SUID binaries
- Mechanisms designed to interfere with security monitoring
- Self-location and self-deletion behavior

The analysis helped establish how the suspicious agent communicates, performs system discovery, and attempts to evade defensive monitoring.

## Key Takeaways

- Static analysis can reveal malware capabilities without executing the sample.
- Embedded strings and symbol names can provide valuable leads during reverse engineering.
- Understanding command handlers helps explain how a malware agent processes remote instructions.
- Attempts to disable tracing or interfere with security tools are important behavioral indicators.
- File hashes and network indicators support malware identification and threat hunting.
- Suspicious binaries should be analyzed in a controlled environment, avoiding execution on production systems.

---

[Back to Sherlocks](./README.md) · [Back to Hack The Box](../README.md)
