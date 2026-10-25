# Dancing — Starting Point (Very Easy)

**Operating System:** Windows  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/395)

## What I Practiced

- Network enumeration with Nmap, identifying RPC (135), NetBIOS (139), and SMB (445).
- Identification of SMB as the primary attack surface.
- Enumeration of available SMB shares using `smbclient`.
- Testing anonymous access without providing a password.
- Accessing the `WorkShares` share without credentials.
- Navigating user directories within the share.
- Downloading files using the SMB `get` command.
- Retrieving the flag from an exposed file.

## Key Takeaways

- SMB enumeration can reveal shared resources and misconfigured permissions.
- Anonymous access should be disabled unless explicitly required and properly restricted.
- File shares must enforce appropriate authentication and access controls.
- Nmap and `smbclient` are useful tools for identifying and investigating exposed SMB resources.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
