# Ignition — Starting Point (Very Easy)

**Operating System:** Linux  
**Web Server:** Nginx  
**Web Application:** Magento  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/405)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of the Nginx web server on TCP port 80.
- Virtual host identification and local hostname resolution using `/etc/hosts`.
- Web application enumeration and directory fuzzing.
- Discovery of the Magento administrative login at `/admin`.
- Identification of weak administrative credentials through password guessing.
- Authentication to the Magento admin panel using the recovered credentials.
- Retrieval of the flag from the administrative interface.

## Key Takeaways

- Virtual host configuration can affect access to web applications.
- Directory enumeration helps uncover administrative interfaces and hidden endpoints.
- Weak administrative passwords can compromise web applications without exploiting a software vulnerability.
- Strong passwords, multi-factor authentication, and login protections help reduce unauthorized access.
- Administrative interfaces should be protected and exposed only as necessary.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
