# Crocodile — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/404)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of FTP on TCP port 21 and HTTP on TCP port 80.
- Detection of anonymous FTP access.
- Enumeration and download of exposed files using the FTP client.
- Analysis of username and password lists to identify exposed credentials.
- Web directory enumeration to discover the `/login.php` endpoint.
- Authentication to the administrative panel using recovered credentials.
- Retrieval of the flag after successful authentication.

## Key Takeaways

- Anonymous FTP access can expose sensitive files when permissions are misconfigured.
- Credentials stored in accessible files can compromise other services on the same host.
- Web directory enumeration helps identify hidden login pages and potential entry points.
- Credentials should never be stored in publicly accessible directories.
- FTP does not encrypt traffic by default; secure file transfer protocols should be preferred.
- Access controls and least-privilege permissions help reduce the risk of credential exposure.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
