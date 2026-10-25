# Cap — Easy Machine

**Difficulty:** Easy  
**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/351)

## What I Practiced

- Network enumeration with Nmap, identifying FTP (port 21), SSH (port 22), and HTTP (port 80).
- Web application enumeration and analysis of a network capture dashboard.
- Identification of an Insecure Direct Object Reference (IDOR) vulnerability.
- Access to another user's packet capture due to insufficient authorization checks.
- PCAP analysis with Wireshark to identify FTP credentials transmitted in plaintext.
- SSH access using the recovered credentials.
- Linux privilege-escalation enumeration.
- Identification of the `cap_setuid` capability assigned to the Python interpreter.
- Privilege escalation to root by abusing the misconfigured Linux capability.
- Retrieval of the user and root flags.

## Key Takeaways

- Applications must enforce server-side authorization when accessing user-specific resources.
- Network captures may expose credentials when authentication protocols transmit data in plaintext.
- Password reuse can allow exposed credentials to compromise other services.
- Linux capabilities must be assigned according to the principle of least privilege.
- Reviewing system capabilities can reveal privilege-escalation opportunities.

---

[Back to Easy Machines](../README.md) · [Back to Hack The Box](../../README.md)
