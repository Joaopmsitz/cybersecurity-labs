# Unified — Starting Point (Very Easy)

**Operating System:** Linux  
**Application:** UniFi Network  
**Key Vulnerabilities:** Log4Shell (CVE-2021-44228), MongoDB misconfiguration  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/441)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of SSH and the UniFi Network web application.
- Application version identification and vulnerability research.
- Analysis and exploitation of Log4Shell (CVE-2021-44228) through JNDI injection.
- Establishment of an initial shell as the `unifi` service account.
- Post-exploitation enumeration of local services and processes.
- Discovery of MongoDB listening on localhost on TCP port 27117 without authentication.
- Enumeration of the `ace` database and its administrator collection.
- Modification of the UniFi administrator password hash to regain access to the web interface.
- Retrieval of device authentication credentials from the UniFi administration settings.
- SSH access as `root` using the recovered credentials.
- Retrieval of both `user.txt` and `root.txt`.

## Key Takeaways

- Unpatched application dependencies can expose systems to critical vulnerabilities such as Log4Shell.
- JNDI injection can lead to remote code execution when vulnerable Log4j configurations are present.
- Database services without authentication can expose sensitive application data and enable account manipulation.
- Localhost-bound services are not directly exposed externally, but may still be accessible after obtaining a shell.
- Reusing database access to modify application accounts can create a path to administrative access.
- Storing device authentication credentials in an application interface increases the impact of an application compromise.
- Patch management, database authentication, least privilege, and secure credential storage help reduce compromise risk.

## Attack Chain

Service Enumeration → Log4Shell (CVE-2021-44228) → Initial Shell as `unifi` → Unauthenticated MongoDB → Administrator Account Manipulation → UniFi Admin Access → SSH Credentials Discovery → Root Access

---

[Back to Tier 2](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
