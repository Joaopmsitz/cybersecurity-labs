# Mongod — Starting Point (Very Easy)

**Operating System:** Linux  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/501)

## What I Practiced

- Network enumeration with Nmap.
- Identification of SSH (port 22) and MongoDB (port 27017).
- MongoDB service enumeration and version identification.
- Connecting to a MongoDB instance without authentication.
- Listing available databases using `show dbs`.
- Selecting the `sensitive_information` database.
- Enumerating database collections using `show collections`.
- Retrieving the flag document using `db.flag.find().pretty()`.
- Identifying the risks of exposing a database without authentication.

## Key Takeaways

- Network enumeration helps identify exposed database services.
- MongoDB instances accessible without authentication may expose sensitive information.
- Database access controls should be explicitly configured and verified.
- Database services should not be exposed publicly unless required and properly secured.
- Restricting network access and enforcing authentication help reduce unauthorized access risks.

---

[Back to Tier 0](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
