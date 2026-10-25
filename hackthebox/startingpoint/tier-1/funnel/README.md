# Funnel — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/520)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of FTP on TCP port 21 and SSH on TCP port 22.
- Enumeration of an FTP server allowing anonymous access.
- Download and analysis of files from the `mail_backup` directory.
- Extraction of a default password from a password policy document.
- Username enumeration and password spraying to identify valid credentials.
- Initial access to the Linux host through SSH as `christine`.
- Enumeration of listening TCP services using `ss`.
- Identification of PostgreSQL listening on localhost on TCP port 5432.
- Creation of an SSH local port-forwarding tunnel to access the database remotely.
- PostgreSQL database enumeration and retrieval of the flag from the `secrets` database.

## Key Takeaways

- Anonymous FTP access can expose internal documents and sensitive information.
- Default passwords should be changed immediately and never reused.
- Password spraying can identify accounts that still use predictable credentials.
- Services bound to localhost are not directly accessible externally, but may be reachable through an authenticated tunnel.
- SSH local port forwarding provides secure access to services through an SSH connection.
- Database access should be restricted through strong authentication, least-privilege permissions, and network controls.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
