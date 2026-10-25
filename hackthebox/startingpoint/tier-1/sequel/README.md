# Sequel — Starting Point (Very Easy)

**Operating System:** Linux  
**Service:** MariaDB  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/403)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of MariaDB running on TCP port 3306.
- Database access using the MySQL command-line client.
- Identification of unauthenticated access as the `root` database user.
- Enumeration of available databases using `SHOW DATABASES`.
- Selection of the `htb` database and enumeration of its tables.
- Querying the `config` table using `SELECT` to retrieve the flag.
- Analysis of insecure database authentication and access controls.

## Key Takeaways

- Exposing a database service to untrusted networks increases the attack surface.
- Database accounts must require strong authentication and follow the principle of least privilege.
- Unauthenticated database access can expose sensitive information and configuration data.
- Database permissions should restrict access to only the resources each account requires.
- Network access to database services should be limited to authorized systems.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
