# Markup — Starting Point (Very Easy)

**Operating System:** Windows  
**Services:** HTTP, SSH  
**Key Vulnerabilities:** XML External Entity (XXE), insecure scheduled task permissions  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/293)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of HTTP on TCP port 80 and SSH on TCP port 22.
- Web application enumeration and authentication testing.
- Analysis of XML processing in the application's order functionality.
- Exploitation of XML External Entity (XXE) to read local files.
- Retrieval of the private SSH key belonging to the user `daniel`.
- SSH access to the Windows host and retrieval of `user.txt`.
- Post-exploitation enumeration using WinPEAS.
- Identification of a scheduled task that runs the batch script `C:\Log-Management\job.bat` with elevated privileges.
- Analysis of insecure file permissions that allow the script to be modified.
- Abuse of the scheduled task to execute commands with Administrator privileges.
- Retrieval of `root.txt`.

## Key Takeaways

- XXE vulnerabilities can expose sensitive local files when XML parsers process untrusted external entities.
- XML parsers should disable external entity resolution unless it is explicitly required.
- Private SSH keys must be protected with appropriate filesystem permissions and passphrases.
- Scheduled tasks can become privilege escalation vectors when their scripts are writable by unprivileged users.
- Administrative scripts should have restrictive permissions and be protected against unauthorized modification.
- Post-exploitation enumeration helps identify misconfigurations that can lead to full system compromise.

## Attack Chain

Network Enumeration → Web Authentication → XXE → SSH Private Key Disclosure → SSH as `daniel` → Scheduled Task Enumeration → Writable Batch Script Abuse → Administrator Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
