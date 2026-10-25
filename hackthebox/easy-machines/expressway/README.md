# Expressway — Easy Machine

**Difficulty:** Easy  
**Operating System:** Linux  
**Status:** Completed

## What I Practiced

- Network enumeration with Nmap, including TCP and UDP scans.
- Identification of SSH on TCP port 22 and IKE/IPsec on UDP port 500.
- IKE service enumeration using `ike-scan`.
- Analysis of IKE Aggressive Mode and pre-shared key authentication.
- Offline PSK hash cracking using `psk-crack` or Hashcat.
- SSH access using recovered credentials.
- Linux privilege-escalation enumeration.
- Identification and exploitation of a vulnerable `sudo` configuration.
- Privilege escalation using CVE-2025-32463.
- Retrieval of the user and root flags.

## Key Takeaways

- TCP-only scans may miss relevant UDP services.
- IKE Aggressive Mode can expose authentication data that enables offline PSK attacks.
- Password reuse can allow credentials recovered from one service to provide access to another.
- Vulnerable `sudo` versions and configurations can enable local privilege escalation.
- Thorough service enumeration and Linux privilege analysis are essential during an investigation.

---

[Back to Easy Machines](../README.md) · [Back to Hack The Box](../../README.md)
