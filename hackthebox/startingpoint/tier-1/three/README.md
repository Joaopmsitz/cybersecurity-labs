# Three — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/489)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Web application enumeration and virtual host discovery.
- Subdomain enumeration to identify the `s3.thetoppers.htb` endpoint.
- Identification of an S3-compatible storage service.
- Interaction with the storage service using the AWS CLI.
- Enumeration of buckets and analysis of access permissions.
- Exploitation of unauthenticated write access to the web-backed storage bucket.
- Upload of a PHP web shell to obtain remote command execution.
- Retrieval of the machine flag from the compromised web server.

## Key Takeaways

- Misconfigured cloud storage permissions can expose sensitive resources and allow unauthorized file uploads.
- S3-compatible services should enforce authentication and appropriate bucket policies.
- Virtual host and subdomain enumeration can reveal additional application components.
- Uploading executable files to a web root can turn a storage misconfiguration into remote code execution.
- Storage permissions and web server execution privileges should follow the principle of least privilege.
- Cloud storage endpoints should not be assumed secure merely because they use an S3-compatible API.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
