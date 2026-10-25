# Hack The Box — Starting Point Tier 2

Tier 2 introduces full penetration testing attack chains, combining service enumeration, initial access, credential discovery, exploitation, and privilege escalation to root or SYSTEM.

## Machines

| Machine | Operating System | Main Focus |
| --- | --- | --- |
| [Archetype](./archetype/) | Windows | SMB credential exposure, MSSQL command execution, and privilege escalation |
| [Oopsie](./oopsie/) | Linux | Broken access control, file upload, and SUID/PATH privilege escalation |
| [Vaccine](./vaccine/) | Linux | Anonymous FTP, password cracking, SQL injection, and `vi` privilege escalation |
| [Unified](./unified/) | Linux | Log4Shell (CVE-2021-44228), MongoDB manipulation, and root access |
| [Included](./Included/) | Linux | LFI/RFI, TFTP file upload, and LXD/LXC privilege escalation |
| [Markup](./markup/) | Windows | XML External Entity (XXE), sensitive file disclosure, and scheduled task abuse |
| [Base](./base/) | Linux | PHP authentication bypass, reverse shell, and `find` privilege escalation |

## Skills Practiced

- Comprehensive network scanning and service enumeration
- SMB, MSSQL, FTP, TFTP, SSH, and database service investigation
- Web application vulnerability analysis, including SQL injection, XXE, LFI, and authentication bypass
- Credential discovery, password cracking, and authentication analysis
- Remote command execution and reverse shell establishment
- Linux privilege escalation through SUID binaries, PATH manipulation, sudo misconfigurations, and LXD/LXC
- Windows privilege escalation through exposed credentials and insecure scheduled tasks
- Attack-chain analysis, evidence collection, and technical documentation

## Learning Objective

Develop an end-to-end penetration testing methodology: identify exposed services, establish initial access, investigate the compromised system, discover privilege escalation paths, and validate the impact of security weaknesses.

Tier 2 machines include two flags: `user.txt` and `root.txt`, representing the progression from initial access to full system compromise.

---

[Back to Starting Point](../README.md) · [Back to Hack The Box](../../README.md)
