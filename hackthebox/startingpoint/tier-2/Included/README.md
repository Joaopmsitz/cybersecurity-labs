# Included — Starting Point (Very Easy)

**Operating System:** Linux  
**Services:** HTTP, TFTP  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/292)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Web application analysis and identification of Local File Inclusion (LFI).
- Reading local system files to gather information about users and directories.
- UDP service enumeration and identification of TFTP.
- Uploading a PHP reverse shell through TFTP.
- Combining LFI with an uploaded payload to obtain initial access as `www-data`.
- Post-exploitation enumeration and discovery of credentials in the `.htpasswd` file.
- Moving from `www-data` to the local user `mike` using recovered credentials.
- Identifying membership in the privileged `lxd` group.
- Exploiting LXD/LXC container configuration to access the host filesystem with root privileges.
- Retrieving both `user.txt` and `root.txt`.

## Key Takeaways

- LFI vulnerabilities can expose sensitive files and, when chained with other weaknesses, contribute to remote code execution.
- TFTP can expose file-transfer functionality without the authentication protections expected from more secure protocols.
- Credentials stored in web-accessible or improperly protected files can enable lateral movement between local accounts.
- Membership in the `lxd` group can provide a path to host-level root access when container privileges are misconfigured.
- File permissions, service restrictions, secure credential storage, and least-privilege group membership are essential security controls.

## Attack Chain

Network Enumeration → LFI → TFTP Payload Upload → PHP Reverse Shell → Credential Discovery → Access as `mike` → LXD/LXC Privilege Escalation → Root Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
