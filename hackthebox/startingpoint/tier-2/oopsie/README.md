# Oopsie — Starting Point (Very Easy)

**Operating System:** Linux  
**Services:** HTTP, SSH  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/288)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Web application enumeration and discovery of `/cdn-cgi/login/`.
- Identification of an IDOR vulnerability to retrieve the administrator's access ID.
- Analysis and manipulation of client-side cookies to bypass access controls.
- Exploitation of broken access control to access administrative upload functionality.
- Upload of a PHP reverse shell to obtain initial access as `www-data`.
- Analysis of application configuration files to discover credentials in `db.php`.
- SSH access as `robert` using the recovered credentials.
- Linux privilege enumeration and identification of the SUID binary `/usr/bin/bugtracker`.
- Exploitation of insecure command execution through PATH hijacking to obtain root privileges.
- Retrieval of both `user.txt` and `root.txt`.

## Key Takeaways

- IDOR vulnerabilities can expose sensitive information when applications fail to enforce object-level authorization.
- Client-controlled cookies must never be trusted as the sole mechanism for enforcing roles or permissions.
- File upload functionality requires strict validation and safe storage of uploaded files.
- Application configuration files can expose credentials when improperly protected.
- SUID binaries that invoke commands without absolute paths may be vulnerable to PATH hijacking.
- Least-privilege execution, secure credential storage, and server-side authorization checks reduce the impact of compromise.

## Attack Chain

Web Enumeration → IDOR → Cookie Manipulation → PHP Reverse Shell → Credential Discovery → SSH as `robert` → SUID Enumeration → PATH Hijacking → Root Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
