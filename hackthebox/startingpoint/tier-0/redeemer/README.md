# Redeemer — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/472)

## What I Practiced

- Network enumeration with Nmap, including a full TCP port scan.
- Identification of Redis running on TCP port 6379.
- Connection to the Redis service using `redis-cli`.
- Enumeration of server information using the `INFO` command.
- Inspection of the keyspace and selection of database 0.
- Listing database keys using `KEYS *`.
- Retrieving the flag using `GET flag`.
- Identification of an exposed database instance without authentication.

## Key Takeaways

- A full port scan can reveal services outside Nmap's default top 1,000 TCP ports.
- Redis is an in-memory key-value data store commonly used for databases, caching, and messaging.
- Unauthenticated Redis access can expose sensitive data and allow unauthorized database operations.
- Database services should enforce appropriate authentication and network access controls.
- Exposing databases to untrusted networks increases the risk of data disclosure and unauthorized modification.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
