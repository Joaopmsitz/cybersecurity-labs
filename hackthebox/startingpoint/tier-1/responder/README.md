# Responder — Starting Point (Very Easy)

**Operating System:** Windows  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/461)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of HTTP on TCP port 80 and WinRM on TCP port 5985.
- Web application enumeration and analysis of the `page` URL parameter.
- Identification of Local File Inclusion (LFI) and Remote File Inclusion (RFI).
- Use of an RFI payload to trigger outbound SMB authentication.
- Capture of a NetNTLMv2 challenge-response using Responder.
- Offline password recovery using John the Ripper.
- Remote Windows access through WinRM using Evil-WinRM.
- Retrieval of the flag from the user's desktop.

## Key Takeaways

- File inclusion vulnerabilities can expose files or trigger unexpected server-side interactions.
- Outbound SMB authentication can expose NetNTLMv2 challenge-response data to an attacker-controlled system.
- Captured NetNTLMv2 responses can be vulnerable to offline password guessing when passwords are weak.
- Strong passwords and appropriately restricted outbound network traffic help reduce credential exposure risks.
- WinRM should be restricted to authorized hosts and protected with strong authentication.
- Web applications should validate file paths and avoid including resources based on untrusted user input.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
