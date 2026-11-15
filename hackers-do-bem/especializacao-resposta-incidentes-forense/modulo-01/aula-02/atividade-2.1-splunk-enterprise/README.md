# Activity 2.1 — Splunk Enterprise

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Start Splunk Enterprise and access its web interface to prepare the environment for security log analysis.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| SIEM | Splunk Enterprise |
| Version | 9.0.3 |
| Host | 192.168.98.10 |
| Web Interface | http://192.168.98.10:8000 |

## Procedure

1. Start the Splunk Enterprise service in the forenseLinux virtual machine.
2. Access the Splunk Web interface through the browser.
3. Authenticate using the administrator account.
4. Open the Search and Reporting application.

The exact service startup command was not preserved in the available notes.

## Observations

The Splunk Enterprise 9.0.3 interface was accessed successfully.

During an initial search involving `/var/log/auth.log`, the interface displayed a license-related error indicating that the Splunk license had expired or that its usage limit had been exceeded too many times.

The search job consequently failed.

Subsequent activity records show that authentication events were available in later searches.

## Result

Splunk Enterprise was started and its web interface was accessed.

The initial license-related error was recorded as an environment limitation encountered during the practical exercise.

## Concepts Practiced

- SIEM platform initialization
- Splunk Web access
- Administrator authentication
- Search and Reporting interface
- Splunk licensing and search execution

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---
[Back to Class 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
