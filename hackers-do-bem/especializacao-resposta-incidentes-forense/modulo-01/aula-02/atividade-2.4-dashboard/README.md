# Activity 2.4 — Linux Monitoring Dashboard in Splunk

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Platform:** Splunk Enterprise 9.0.3
> **Status:** Completed

## 1. Objective

Create a Splunk dashboard to centralize Linux authentication events and provide a visual interface for monitoring account-related activity.

Dashboards support security monitoring by presenting search results in an organized and accessible interface.

## 2. Environment

| Item | Details |
|---|---|
| SIEM | Splunk Enterprise 9.0.3 |
| Host | ip-192-168-98-10 |
| Log Source | /var/log/auth.log |
| Sourcetype | linux_secure |
| Dashboard Title | Painel de monitoramento |
| Subtitle | Monitoramento |
| Application | search |

## 3. Procedure

### Step 1 — Open the Dashboard Interface

Access the Dashboards area in Splunk Enterprise.

### Step 2 — Create a Dashboard

Create a dashboard named:

```text
Painel de monitoramento
```

The screenshot transcription also records the subtitle:

```text
Monitoramento
```

### Step 3 — Add the Monitoring Search

The activity report describes adding the authentication log search to the dashboard.

The available transcription does not preserve the complete search expression used by the dashboard panel.

The dashboard was associated with Linux authentication records from:

```text
/var/log/auth.log
```

### Step 4 — Save and Review the Dashboard

Save the dashboard and inspect the displayed records.

The screenshot transcription identifies the dashboard URL path as:

```text
/en-US/app/search/painel_de_monitoramento
```

## 4. Observed Dashboard Events

The available screenshot transcription from May 8, 2026, at approximately 21:08 contains the following events.

### Event 1 — Root Session Closed

```text
2026-05-08T21:03:58.050452-03:00 ip-192-168-98-10 sudo: pam_unix(sudo: session): session closed for user root
```

### Event 2 — Group Membership Updated

```text
2026-05-08T21:03:58.023820-03:00 ip-192-168-98-10 gpasswd[10952]: members of group users set by root to exemplo, exemplo2
```

### Event 3 — User Information Modified

```text
2026-05-08T21:03:56.824253-03:00 ip-192-168-98-10 chfn[10909]: changed user 'exemplo2' information
```

### Event 4 — Keyring Warning

```text
2026-05-08T21:03:53.973040-03:00 ip-192-168-98-10 passwd[10881]: gkr-pam: couldn't update the login keyring password: no old password was entered
```

### Event 5 — Password Change Recorded

```text
2026-05-08T21:03:53.969768-03:00 ip-192-168-98-10 passwd[10881]: pam_unix(passwd:chauthtok): password changed for exemplo2
```

### Event 6 — New User Created

```text
2026-05-08T21:03:48.276420-03:00 ip-192-168-98-10 useradd[10872]: new user: name exemplo2, UID=1005, GID=1005, home /home/exemplo2, shell /bin/bash, from /dev/pts/1
```

## 5. User Account Attributes

The event associated with `exemplo2` records:

| Attribute | Value |
|---|---|
| Username | exemplo2 |
| UID | 1005 |
| GID | 1005 |
| Home Directory | /home/exemplo2 |
| Login Shell | /bin/bash |
| Execution Context | /dev/pts/1 |

The records provide visibility into account creation and the subsequent modifications.

## 6. Event Analysis

The dashboard groups several records associated with the user creation process.

| Process | Event |
|---|---|
| useradd | Account creation |
| passwd | Password change |
| chfn | Account information update |
| gpasswd | Group membership update |
| sudo | Privileged session closure |

These events provide a timeline of account-related activity.

The sequence demonstrates why correlation across multiple log records is important.

An account creation event alone may not explain all subsequent actions, while related password and group events provide additional context.

## 7. Technical Interpretation

A Splunk dashboard associates searches with display components.

Search results can be shown as tables or visualizations, depending on the configured panel and the data available.

In this activity, the dashboard provided a centralized view of Linux authentication events.

The dashboard's primary value is not merely visualization; it also supports faster navigation between events during an investigation.

## 8. Results

The activity report records that the dashboard was created and saved as:

```text
Painel de monitoramento
```

The dashboard displayed account-related events associated with `exemplo2`.

The available records demonstrate that the dashboard was able to present authentication log events from the Linux host.

## 9. Concepts Practiced

- Splunk dashboards
- Search result visualization
- Linux authentication monitoring
- Account lifecycle investigation
- Event timelines
- Privileged activity monitoring
- SIEM dashboard organization
- Security monitoring

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The evidence document includes the monitoring dashboard and the displayed account-management records.

## References

- [Splunk Dashboard Studio](https://help.splunk.com/en/splunk-enterprise/create-dashboards-and-reports/dashboard-studio)
- [Adding and Formatting Visualizations](https://help.splunk.com/en/splunk-enterprise/create-dashboards-and-reports/dashboard-studio/9.0/visualizations/add-and-format-visualizations)

---

[Back to Class 02](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
