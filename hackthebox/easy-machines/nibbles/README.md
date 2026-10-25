# Nibbles — Easy Machine

**Operating System:** Linux  
**Difficulty:** Easy  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/121)

## What I Practiced

- Network enumeration with Nmap, identifying SSH (port 22) and HTTP (port 80).
- Web enumeration to discover the NibbleBlog application and administrative interface.
- Directory and file discovery using Gobuster/Dirb.
- Identification of weak administrative credentials (`admin:nibbles`).
- Exploitation of an unrestricted file upload vulnerability to obtain a PHP reverse shell.
- Initial access to the Linux target system.
- Transfer and execution of LinEnum for privilege-escalation enumeration.
- Analysis of sudo permissions and identification of a privilege-escalation path.
- Exploitation of a misconfigured sudo rule to obtain root access.
- Retrieval of the root flag and completion of the machine.

## Key Takeaways

- Thorough enumeration helps identify hidden applications and exposed resources.
- Weak credentials can compromise administrative interfaces.
- Unrestricted file uploads can lead to remote code execution.
- Scripts executable through misconfigured sudo rules can introduce privilege-escalation risks.
- Proper access controls, secure file-upload validation, and least-privilege configurations help reduce these risks.

---

[Back to Easy Machines](../README.md) · [Back to Hack The Box](../../README.md)
