# Fawn — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/393)

## What I Practiced

- Network enumeration with Nmap.
- Identification of the FTP service on TCP port 21.
- Detection of anonymous FTP login enabled on the server.
- Accessing FTP using the `anonymous` account without a password.
- Listing remote files and directories using FTP commands.
- Downloading `flag.txt` using the FTP `get` command.
- Retrieving the flag through an exposed file share.

## Key Takeaways

- Network enumeration helps identify exposed services and potential security weaknesses.
- Anonymous FTP access can expose files to unauthorized users.
- FTP transfers data without encryption, potentially exposing credentials and file contents.
- FTP directory permissions should restrict access to authorized users.
- SFTP or properly configured FTPS should be preferred for secure file transfers.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
