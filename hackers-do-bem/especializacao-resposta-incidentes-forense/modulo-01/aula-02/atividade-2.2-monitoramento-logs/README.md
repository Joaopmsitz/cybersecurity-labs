# Activity 2.2 — Linux Authentication Log Monitoring

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 01  
> **Class:** 02  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## Objective

Monitor Linux authentication events using Splunk Enterprise and analyze log records generated during user account creation and modification.

## Environment

| Item | Details |
|---|---|
| SIEM | Splunk Enterprise 9.0.3 |
| Host | 192.168.98.10 |
| Log Source | /var/log/auth.log |
| Sourcetype | linux_secure |

## Search Query

The following search was recorded in Splunk:

```spl
source="/var/log/auth.log" host="ip-192-168-98-10" sourcetype="linux_secure"
```

The search returned Linux authentication events associated with the host.

## Procedure

A new Linux user named `exemplo` was created to generate authentication and account-management events.

The resulting records were examined through Splunk.

## Observed Events

The activity transcription contains the following events from May 8, 2026:

| Time | Process | Observed Event |
|---|---|---|
| 20:52:09 | groupadd | Created group `exemplo`, GID 1004 |
| 20:52:09 | useradd | Created user `exemplo`, UID 1004 |
| 20:52:14 | passwd | Password change recorded |
| 20:52:54 | chfn | User information modified |
| 20:52:58 | gpasswd | Group membership updated |
| 20:52:58 | sudo | Root session closed |

The created account had the following recorded attributes:

- Username: `exemplo`
- UID: `1004`
- GID: `1004`
- Home directory: `/home/exemplo`
- Login shell: `/bin/bash`

A `gkr-pam` keyring warning was also present alongside the password-change events.

## Result

Splunk displayed authentication and account-management events from `/var/log/auth.log`.

The records demonstrated how user creation and subsequent account modifications generate traceable security events.

## Concepts Practiced

- Authentication log monitoring
- Linux user and group management
- Event correlation
- Account activity investigation
- SIEM search and filtering
- Security event interpretation

---

[Back to Class 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
