# Archetype — Starting Point (Very Easy)

**Operating System:** Windows  
**Services:** SMB, Microsoft SQL Server  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/287)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of SMB on TCP port 445 and Microsoft SQL Server on TCP port 1433.
- Enumeration of SMB shares and identification of anonymous access to the `backups` share.
- Download and analysis of `prod.dtsConfig`, which contained plaintext database credentials.
- Authentication to Microsoft SQL Server using Impacket's `mssqlclient.py`.
- Enabling `xp_cmdshell` to execute operating system commands through SQL Server.
- Establishment of a reverse shell to obtain initial access as the `sql_svc` service account.
- Post-exploitation enumeration using WinPEAS to identify privilege escalation opportunities.
- Discovery of the Administrator password in the PowerShell history file `ConsoleHost_history.txt`.
- Privilege escalation to Administrator using the recovered credentials.
- Retrieval of both `user.txt` and `root.txt`.

## Key Takeaways

- Anonymous SMB access can expose sensitive configuration files and plaintext credentials.
- Database connection strings should never contain unprotected credentials in accessible files.
- Enabling `xp_cmdshell` can turn a database compromise into operating system command execution.
- PowerShell history files may retain sensitive commands and credentials.
- Post-exploitation enumeration helps identify paths to higher privileges.
- Strong credential management, restricted share permissions, and least-privilege access reduce the impact of compromise.

## Attack Chain

SMB Enumeration → Credential Discovery → MSSQL Access → `xp_cmdshell` → Reverse Shell → PowerShell History Analysis → Administrator Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
