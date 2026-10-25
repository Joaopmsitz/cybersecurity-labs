# Explosion — Starting Point (Very Easy)

**Operating System:** Windows  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/396)

## What I Practiced

- Network enumeration with Nmap, identifying RPC (135), NetBIOS (139), SMB (445), and RDP (3389).
- Identification of Remote Desktop Protocol (RDP) as the primary access vector.
- Connection to a remote Windows system using an RDP client.
- Investigation of insecure authentication configuration.
- Access to the system using the `Administrator` account with a blank password.
- Basic Windows desktop navigation and flag retrieval.

## Key Takeaways

- Network enumeration helps identify exposed services and potential entry points.
- RDP should enforce strong authentication and appropriate network access controls.
- Administrator accounts must never be left without a password.
- Exposed remote administration services increase the risk of unauthorized access.
- SMB and RPC may be present on the host without being the primary attack path.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
