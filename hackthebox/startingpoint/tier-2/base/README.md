# Base — Starting Point (Very Easy)

**Operating System:** Linux  
**Services:** HTTP, SSH  
**Key Vulnerabilities:** PHP authentication bypass, unrestricted file upload, sudo misconfiguration  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/479)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of HTTP on TCP port 80 and SSH on TCP port 22.
- Web directory enumeration to discover the `/login/` directory.
- Discovery and analysis of the exposed `login.php.swp` file.
- Analysis of PHP authentication logic and identification of an insecure `strcmp()` comparison.
- Authentication bypass using PHP array parameters.
- Access to the file upload functionality after bypassing authentication.
- Upload and execution of a PHP reverse shell to obtain initial access as `www-data`.
- Analysis of application configuration files to recover credentials.
- SSH access as the local user `john`.
- Enumeration of sudo permissions and identification of `/usr/bin/find` as a permitted command.
- Privilege escalation by abusing `find` with its `-exec` option to obtain a root shell.
- Retrieval of both `user.txt` and `root.txt`.

## Key Takeaways

- Exposed source code and leftover editor swap files can reveal sensitive application logic.
- Insecure PHP comparisons can allow authentication bypass when input types are not handled correctly.
- File upload functionality can become a remote code execution vector when uploaded scripts are executable by the web server.
- Credentials stored in application configuration files should be protected and never reused across accounts.
- Sudo permissions on commands such as `find` can allow privilege escalation when those commands can execute arbitrary programs.
- Secure coding, restrictive file permissions, strong credential management, and least-privilege access reduce the risk of compromise.

## Attack Chain

Network Enumeration → Exposed PHP Source (`login.php.swp`) → Authentication Bypass → PHP Reverse Shell → Credential Discovery → SSH as `john` → Sudo Abuse of `find` → Root Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
