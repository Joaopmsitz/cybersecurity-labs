# Brutus — Sherlock (Very Easy)

**Category:** Digital Forensics & Incident Response (DFIR)  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/631)

## Overview

Brutus is a Sherlock challenge focused on Linux log forensics and SSH authentication investigation.

The scenario involves suspected system compromise following SSH brute-force activity. The investigation uses authentication logs and session records to reconstruct the attack timeline and identify suspicious activity.

## Investigation Focus

- Linux authentication log analysis (`auth.log`)
- Session history analysis using `wtmp`
- SSH authentication and brute-force detection
- Identification of suspicious source IP addresses
- Correlation of failed and successful login attempts
- Investigation of post-compromise activity
- Analysis of user creation and potential persistence indicators
- Timeline reconstruction using Linux command-line tools

## Tools Used

- Linux command-line utilities
- `grep`
- `sort`
- `uniq`
- `last`
- `auth.log`
- `wtmp`

## Investigation Summary

The investigation involved correlating authentication logs and session records to examine suspicious SSH activity.

The analysis focused on identifying repeated authentication failures, determining when successful access occurred, and examining subsequent activity to reconstruct the sequence of events.

## Key Takeaways

- Authentication logs are valuable sources of evidence during Linux security investigations.
- Correlating failed and successful logins helps identify potential brute-force compromises.
- Session records provide additional context for reconstructing user activity.
- Timeline reconstruction helps establish the sequence of suspicious events.
- Investigative conclusions should be supported by evidence from the available log sources.

---

[Back to Sherlocks](./README.md) · [Back to Hack The Box](../README.md)
