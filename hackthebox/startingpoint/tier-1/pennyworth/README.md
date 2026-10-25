# Pennyworth — Starting Point (Very Easy)

**Operating System:** Linux  
**Service:** Jenkins  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/406)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of the HTTP service on TCP port 8080.
- Web application fingerprinting to identify Jenkins running on Jetty.
- Identification of weak administrative credentials.
- Authentication to Jenkins using the credentials `root:password`.
- Exploration of the Jenkins Script Console.
- Use of Groovy scripting to execute commands on the underlying Linux system.
- Establishment of a reverse shell to obtain remote command-line access.
- Retrieval of the flag from `/root/flag.txt`.

## Key Takeaways

- Weak credentials can expose administrative interfaces to unauthorized access.
- Jenkins Script Console access can allow arbitrary code execution on the host.
- CI/CD platforms require strong authentication and strict access controls.
- Administrative scripting capabilities should be restricted to trusted users.
- Services should run with the least privileges necessary to reduce the impact of compromise.
- Exposed management interfaces should be restricted to authorized networks.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
