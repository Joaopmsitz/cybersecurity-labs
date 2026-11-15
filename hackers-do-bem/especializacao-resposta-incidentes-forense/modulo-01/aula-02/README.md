# Hackers do Bem — Specialization | Module 01 — Class 02

This class explores security event monitoring and incident investigation using Splunk Enterprise and Linux authentication logs. The activities cover log searches, user and group activity analysis, alert configuration, dashboard development, and security monitoring use cases.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 02 |
| Activities | 5 |
| Main Topics | Security Information and Event Management (SIEM), Linux Authentication Logs, SPL, Security Alerts, Dashboards, and Incident Investigation |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|

## Environment

The activities used Splunk Enterprise running on the `forenseLinux` virtual machine.

| Component | Details |
|---|---|
| Virtual Machine | forenseLinux |
| Host Address | 192.168.98.10 |
| Splunk Version | 9.0.3 |
| Web Interface | Port 8000 |
| Main Log Source | `/var/log/auth.log` |
| Sourcetype | `linux_secure` |
| Search Language | Search Processing Language (SPL) |

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| SIEM Platform | Splunk Enterprise 9.0.3 | Centralize, search, and investigate security events. |
| Log Sources | Linux auth.log, linux_secure | Provide authentication and account management telemetry. |
| Search Language | Splunk SPL | Filter, investigate, and transform security events. |
| Alerting | Splunk Alerts | Identify events that match defined detection conditions. |
| Visualization | Splunk Dashboards | Present security events and monitoring information. |

## Learning Outcomes

- Understand the role of a SIEM platform in security monitoring.
- Search and investigate Linux authentication logs.
- Identify account creation and privilege-related activities.
- Create alerts based on security event conditions.
- Build dashboards to visualize security telemetry.
- Use SPL to filter and organize investigation results.

## Evidence Requirements

The original practical assignment consolidates the required evidence into a single PDF document.

[View Universal Class Evidence PDF](./evidences.pdf)

The universal class evidence PDF consolidates the screenshots documenting the Splunk searches, alert configuration, dashboard, and investigation results.

## Technical Notes

- The initial search recorded in the activity report returned a Splunk license-expired or license-limit error. Later screenshots documented authentication events successfully. These are separate observations; the documentation does not assume an undocumented cause for the change.
- The investigation included account creation, password and group modifications, and sudo-related command activity.
- The alert and dashboard exercises demonstrate monitoring capabilities. A configured alert should not be interpreted as proof that every matching event represents malicious activity.

## References

- [Splunk Enterprise — Search and Reporting](https://help.splunk.com/en/splunk-enterprise/get-started/overview/10.2/splunk-enterprise-resources-and-documentation/search-and-reporting)
- [Splunk Enterprise — Search Reference](https://help.splunk.com/en/splunk-enterprise/search/spl-search-reference/9.4/introduction/welcome-to-the-search-reference)
- [Splunk — Creating Alerts](https://help.splunk.com/en/splunk-enterprise/search/spl2-search-manual/creating-reports-alerts-and-dashboards/create-an-alert-using-an-spl2-search)
- [Splunk — Creating Dashboards](https://help.splunk.com/en/splunk-enterprise/search/spl2-search-manual/creating-reports-alerts-and-dashboards/create-a-dashboard-using-an-spl2-search)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
