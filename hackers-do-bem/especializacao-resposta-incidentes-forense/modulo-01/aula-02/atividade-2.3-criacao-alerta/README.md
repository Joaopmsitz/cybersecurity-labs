# Activity 2.3 — Splunk Alert Configuration

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 01  
> **Class:** 02  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## Objective

Configure a Splunk alert to monitor the use of the Linux `adduser` command and identify user creation activity.

## Alert Configuration

The following configuration was recorded:

| Property | Value |
|---|---|
| Alert Name | Uso do adduser |
| Description | Cada vez que o comando adduser for utilizado. |
| Status | Enabled |
| Application | search |
| Permissions | Private |
| Alert Type | Real-time |
| Trigger Condition | Per-Result |
| Actions | 1 configured action |
| Last Modified | May 8, 2026 — 21:03:05 |

## Procedure

1. Configure an alert in Splunk to monitor the use of `adduser`.
2. Set the alert to real-time execution.
3. Configure the trigger condition as Per-Result.
4. Save and enable the alert.
5. Create the Linux user `exemplo2` to generate another account-management event.

## Observations

The alert configuration was recorded in Splunk.

The activity report describes the creation of `exemplo2` as the test used to trigger the alert.

However, the available alert-management screenshot displayed:

`There are no fired events for this alert.`

A subsequent dashboard record showed the creation of `exemplo2` at approximately 21:03:48 on May 8, 2026.

The available records therefore confirm the alert configuration and the subsequent user creation, but do not independently establish that the alert history registered a trigger.

## Result

A real-time Splunk alert was configured to monitor user creation activity.

The available records document the configuration and test event, with the alert-trigger status noted as an evidence limitation.

## Concepts Practiced

- SIEM alert configuration
- Real-time event monitoring
- Per-result trigger conditions
- Account creation detection
- Security monitoring and alert validation

---

[Back to Class 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
