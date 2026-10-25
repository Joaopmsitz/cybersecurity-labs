# TwoMillion — Easy Machine

**Difficulty:** Easy  
**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/547)

## What I Practiced

- Network enumeration with Nmap, identifying SSH (port 22) and HTTP (port 80).
- Web application and API enumeration.
- Analysis of the invite-code generation mechanism.
- Identification of broken access control in the administrative API.
- Privilege escalation to an application administrator.
- Command injection in the VPN profile generation endpoint.
- Configuration file analysis and identification of exposed credentials.
- Credential reuse analysis and access to the local user account.
- Linux privilege escalation and root access.
- Retrieval of the user and root flags.

## Key Takeaways

- Client-side logic should never be treated as a security boundary.
- Administrative API endpoints must enforce server-side authorization.
- Unsanitized user input passed to operating system commands can lead to command injection.
- Sensitive credentials must not be exposed in application configuration files.
- Password reuse can turn an application-level compromise into a system-level compromise.
- Unpatched software may expose additional privilege-escalation paths.

---

[Back to Easy Machines](../README.md) · [Back to Hack The Box](../../README.md)
