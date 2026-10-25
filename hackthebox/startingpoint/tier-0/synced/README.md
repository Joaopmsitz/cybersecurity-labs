# Synced — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/515)

## What I Practiced

- Network enumeration with Nmap.
- Identification of the rsync service on TCP port 873.
- Service version detection and protocol identification.
- Enumeration of available rsync modules.
- Listing files using the `--list-only` option.
- Accessing the `public` module without authentication.
- Downloading `flag.txt` using rsync.
- Retrieving the flag from an anonymously accessible file.

## Key Takeaways

- Network enumeration helps identify exposed services and their potential risks.
- Rsync modules may expose files when anonymous access is improperly configured.
- File synchronization services should enforce appropriate authentication and access controls.
- Restricting network exposure reduces unauthorized access to shared resources.
- Reviewing module permissions helps prevent sensitive data disclosure.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
