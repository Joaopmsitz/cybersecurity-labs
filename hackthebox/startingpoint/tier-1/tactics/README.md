# Tactics — Starting Point (Very Easy)

**Operating System:** Windows  
**Service:** SMB  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/407)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of SMB on TCP port 445.
- Enumeration of available SMB shares using `smbclient`.
- Testing authentication with the `Administrator` account and a blank password.
- Identification of a misconfigured account allowing passwordless access.
- Enumeration of administrative shares, including `C$`.
- Navigation through the Windows filesystem via SMB.
- Retrieval of `flag.txt` from `C:\Users\Administrator\Desktop`.

## Key Takeaways

- SMB administrative shares can expose an extensive portion of a Windows filesystem.
- Allowing an Administrator account to authenticate without a password can lead to complete system compromise.
- Administrative shares should only be accessible to authorized accounts and trusted systems.
- Strong authentication and least-privilege access controls are essential for Windows systems.
- Network exposure of SMB should be restricted to the systems that require it.
- Service enumeration can reveal security misconfigurations even when no software exploit is necessary.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
