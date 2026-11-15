# Activity 2.3 — Real-Time Alert Configuration in Splunk

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Platform:** Splunk Enterprise 9.0.3
> **Status:** Completed

## 1. Objective

Create a real-time Splunk alert to monitor Linux account creation activity involving the `adduser` command.

The purpose is to demonstrate how SIEM alerting can identify events that may require further investigation.

## 2. Environment

| Item | Details |
|---|---|
| SIEM | Splunk Enterprise 9.0.3 |
| Host | ip-192-168-98-10 |
| Log Source | /var/log/auth.log |
| Sourcetype | linux_secure |
| Alert Name | Uso do adduser |
| Trigger Type | Real-time |
| Trigger Condition | Per-Result |

## 3. Alert Configuration

The available configuration screenshot records:

| Property | Recorded Value |
|---|---|
| Title | Uso do adduser |
| Description | Cada vez que o comando adduser for utilizado. |
| Enabled | Yes |
| Application | search |
| Permissions | Private |
| Owner | admin |
| Modified | May 8, 2026 — 9:03:05 PM |
| Alert Type | Real-time |
| Trigger Condition | Per-Result |
| Actions | 1 configured action |

The alert was enabled and saved under the Search application.

The exact underlying SPL search and the details of the configured action were not preserved in the available transcription.

They are therefore not reconstructed as confirmed settings.

## 4. Procedure

### Step 1 — Prepare the Search

Use authentication events from:

```text
/var/log/auth.log
```

The monitoring objective is to identify the account creation activity associated with `adduser`.

The original activity notes do not preserve the complete alert search expression.

### Step 2 — Save the Search as an Alert

From the Splunk search interface:

1. Open the search results.
2. Select the option to save the search as an alert.
3. Set the title to:

```text
Uso do adduser
```

4. Configure the description:

```text
Cada vez que o comando adduser for utilizado.
```

5. Enable the alert.

### Step 3 — Configure Real-Time Triggering

The screenshot records:

```text
Alert Type: Real-time
Trigger Condition: Per-Result
```

A per-result real-time alert uses a continuous search and triggers when individual search results match the triggering criteria.

This means each qualifying result can generate an alert.

### Step 4 — Configure an Alert Action

The screenshot shows:

```text
Actions: 1 Action
```

The exact action type is not preserved in the available notes.

### Step 5 — Create a Test Account

The activity report describes creating the Linux account:

```text
exemplo2
```

The subsequent dashboard records show the creation event.

### Step 6 — Review Triggered Events

The alert management screenshot displayed:

```text
There are no fired events for this alert.
```

This observation is important because it does not independently confirm that the configured alert successfully triggered.

## 5. Recorded Test Event

The subsequent dashboard transcription contains the following event:

```text
2026-05-08T21:03:48.276420-03:00 ip-192-168-98-10 useradd[10872]: new user: name exemplo2, UID=1005, GID=1005, home /home/exemplo2, shell /bin/bash, from /dev/pts/1
```

The account creation event demonstrates that the system recorded the creation of `exemplo2`.

## 6. Important Technical Distinction

The alert description refers to:

```text
adduser
```

The recorded authentication event contains:

```text
useradd
```

These are related account-management utilities, but the recorded event name should not be treated as direct evidence that the exact `adduser` command was executed.

A reliable alert should be validated against the actual event fields and process information available in the logs.

## 7. Analysis of the Recorded Results

Two different observations are available:

| Source | Observation |
|---|---|
| Alert Management | No fired events for this alert |
| Dashboard | `exemplo2` account creation event recorded |

The dashboard confirms the user creation event, while the alert management screenshot does not confirm a corresponding trigger.

Possible reasons include differences between the alert search expression, event format, time range, triggering criteria, or alert execution.

The exact cause cannot be established from the available screenshots.

## 8. Real-Time Alert Concepts

Real-time alerts are useful when an organization needs to monitor events as they happen.

Per-result triggering means that individual matching results can trigger the configured alert.

Real-time searches can be resource-intensive because they continuously evaluate incoming events.

The alert configuration should therefore be validated against realistic data and an appropriate search expression.

## 9. Results

The activity report records that the `Uso do adduser` alert was created and enabled.

It also documents the creation of `exemplo2` as a test event.

The available alert management screenshot showed no fired events at the time it was captured.

The configuration was documented, but successful alert triggering is not claimed as independently verified.

## 10. Concepts Practiced

- Splunk alert creation
- Real-time monitoring
- Per-result triggering
- Linux account creation detection
- Alert actions
- Triggered-event investigation
- Detection validation
- SIEM monitoring

## 11. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The evidence document includes the alert configuration and its recorded state.

## References

- [Splunk — Create Real-Time Alerts](https://help.splunk.com/en/splunk-enterprise/alert-and-respond/alerting-manual/9.3/create-alerts/create-real-time-alerts)
- [Splunk Alert Documentation](https://help.splunk.com/en/splunk-enterprise/alert-and-respond/alerting-manual)

---

[Back to Class 02](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
