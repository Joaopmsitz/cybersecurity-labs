# Vaccine — Starting Point (Very Easy)

**Operating System:** Linux  
**Services:** FTP, SSH, HTTP  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/289)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of FTP on TCP port 21, SSH on TCP port 22, and HTTP on TCP port 80.
- Enumeration of an FTP service allowing anonymous access.
- Download of the password-protected `backup.zip` archive.
- Password recovery using `zip2john` and John the Ripper.
- Analysis of the extracted PHP source code to identify application credentials.
- Recovery of the web administrator password from an MD5 hash.
- Authentication to the web application and analysis of its search functionality.
- Identification and exploitation of SQL injection using sqlmap.
- Use of sqlmap's `--os-shell` option to obtain command execution and an initial shell as `postgres`.
- Analysis of application configuration files to recover the PostgreSQL user's password.
- SSH access as `postgres` for a more stable shell.
- Enumeration of sudo permissions and identification of the restricted `vi` command.
- Privilege escalation by escaping the `vi` editor to obtain a root shell.
- Retrieval of both `user.txt` and `root.txt`.

## Key Takeaways

- Anonymous FTP access can expose sensitive backup archives.
- Password-protected archives and weak passwords can be vulnerable to offline cracking.
- Hardcoded credentials and weak password hashing can expose web applications to compromise.
- SQL injection may lead to operating system command execution, depending on the application's database configuration and privileges.
- Configuration files and application source code can expose additional credentials.
- Restricting sudo permissions is not sufficient if an allowed program can spawn a privileged shell.
- Least privilege, secure credential storage, parameterized SQL queries, and restricted service access help reduce compromise risk.

## Attack Chain

FTP Enumeration → ZIP Password Cracking → Credential Discovery → Web Login → SQL Injection → OS Command Execution → SSH as `postgres` → Sudo Misconfiguration in `vi` → Root Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
