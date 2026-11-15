# Activity 2.5 — Security Monitoring Use Cases

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Explore Splunk searches for security monitoring and investigate Linux system activity associated with privileged commands and potential security incidents.

## Monitoring Scenarios

The activity report describes searches covering the following use cases:

- Root user activity
- Suspicious process execution
- Changes to critical files
- Network connections
- Privilege escalation

The available transcription preserves the exact search for root-command activity.

## Recorded SPL Query

```spl
index=* sourcetype="linux_secure" source="/var/log/auth.log" "COMMAND=" "USER=root"
| table _time, host, cmd
```

The search filters Linux authentication events containing command-execution information associated with the root user.

The `table` command organizes the results into the following fields:

- `_time`: Event timestamp
- `host`: Source host
- `cmd`: Recorded command

## Search Results

The recorded search used the `Last 24 hours` time range.

The available transcription reports:

| Item | Result |
|---|---|
| Events Returned | 17 |
| Host | ip-192-168-98-10 |
| Source | /var/log/auth.log |
| Sourcetype | linux_secure |
| Time Range | Last 24 hours |

The event records span May 7–8, 2026.

The available notes preserve the search configuration and result count, but not the complete output or separate SPL queries for every monitoring scenario.

## Result

The activity explored the use of Splunk searches to investigate privileged command execution and other security monitoring scenarios.

The recorded SPL query demonstrates how authentication logs can be filtered and organized to support the investigation of root activity.

## Concepts Practiced

- Security monitoring use cases
- SPL search language
- Root activity investigation
- Privileged command monitoring
- Log filtering and field selection
- Event analysis and investigation

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---
[Back to Class 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
