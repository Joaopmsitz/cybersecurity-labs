# Activity 2.4 — Splunk Monitoring Dashboard

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 01  
> **Class:** 02  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## Objective

Create a Splunk dashboard to centralize the visualization of Linux authentication events and support ongoing security monitoring.

## Dashboard Configuration

| Property | Value |
|---|---|
| Dashboard Title | Painel de monitoramento |
| Subtitle | Monitoramento |
| Application | search |
| Data Source | /var/log/auth.log |
| Sourcetype | linux_secure |

## Procedure

1. Open the Splunk dashboard interface.
2. Create a new dashboard named `Painel de monitoramento`.
3. Configure the dashboard subtitle as `Monitoramento`.
4. Add the authentication log search to the dashboard.
5. Save the dashboard and inspect the displayed events.

## Observed Events

The dashboard displayed account-management events from May 8, 2026.

Examples recorded in the activity transcription include:

| Time | Process | Observed Event |
|---|---|---|
| 21:03:48 | useradd | Created user `exemplo2` |
| 21:03:53 | passwd | Password change recorded for `exemplo2` |
| 21:03:56 | chfn | Modified user information |
| 21:03:58 | gpasswd | Updated group membership |
| 21:03:58 | sudo | Root session closed |

The second user account had the following recorded attributes:

- Username: `exemplo2`
- UID: `1005`
- GID: `1005`
- Home directory: `/home/exemplo2`

## Result

The dashboard was saved and displayed Linux authentication events associated with user account creation and modification.

Centralizing these events provides a convenient view of activity relevant to security monitoring and incident investigation.

## Concepts Practiced

- Splunk dashboards
- Security event visualization
- Authentication monitoring
- Log aggregation
- Security operations monitoring

---

[Back to Class 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
