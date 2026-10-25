# Hack The Box — Starting Point Tier 2

Tier 2 introduces multi-stage penetration testing scenarios that combine service enumeration, initial access, credential discovery, exploitation, and privilege escalation to root or SYSTEM.

## Machines

| Machine | Operating System | Main Focus | Status |
| --- | --- | --- | --- |
| [Archetype](./archetype/) | Windows | SMB credential exposure, MSSQL command execution, and privilege escalation | Completed |
| [Oopsie](./oopsie/) | Linux | IDOR, file upload, and SUID/PATH privilege escalation | Completed |
| [Vaccine](./vaccine/) | Linux | Anonymous FTP, password cracking, SQL injection, and `vi` privilege escalation | Completed |
| [Unified](./unified/) | Linux | Log4Shell (CVE-2021-44228), unauthenticated MongoDB, and credential recovery | Completed |
| [Included](./Included/) | Linux | LFI, TFTP payload transfer, and LXD/LXC privilege escalation | Completed |
| [Markup](./markup/) | Windows | XML External Entity (XXE), SSH key disclosure, and scheduled task abuse | Completed |
| [Base](./base/) | Linux | PHP authentication bypass, reverse shell, and `sudo`/`find` privilege escalation | Completed |

## Skills Practiced

- Comprehensive network scanning and service enumeration
- Investigation of SMB, MSSQL, FTP, TFTP, SSH, HTTP, and database services
- Web application vulnerability analysis, including SQL injection, XXE, LFI, and authentication bypass
- Credential discovery, password cracking, and authentication analysis
- Remote command execution and reverse shell establishment
- Linux privilege escalation through SUID/PATH abuse, sudo misconfigurations, and LXD/LXC permissions
- Windows privilege escalation through exposed credentials and insecure scheduled tasks
- Attack-chain analysis, evidence collection, and technical documentation

## Learning Objective

Develop an end-to-end penetration testing methodology: identify exposed services, establish initial access, investigate the compromised system, discover privilege escalation paths, and validate the impact of security weaknesses.

Each Tier 2 machine has two flags: `user.txt` and `root.txt`, representing the progression from initial access to full system compromise.

---

[Back to Starting Point](../README.md) · [Back to Hack The Box](../../README.md)
