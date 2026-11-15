# Hackers do Bem — Specialization | Module 01 — Class 02

Detailed documentation of the practical activities from Class 02 of the Hackers do Bem Incident Response and Digital Forensics specialization.

This class introduces security monitoring and incident investigation through Splunk Enterprise, using Linux authentication logs, alerts, dashboards, and security-focused searches.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 02 |
| Activities | 5 |
| Environment | forenseLinux VM |
| Platform | Splunk Enterprise 9.0.3 |
| Host | 192.168.98.10 |

## Practical Activities

| Activity | Topic | Documentation |
|---|---|---|
| 2.1 | Splunk Enterprise | [View Activity](./atividade-2.1-splunk-enterprise/) |
| 2.2 | Linux Authentication Log Monitoring | [View Activity](./atividade-2.2-monitoramento-logs/) |
| 2.3 | Real-Time Alert Configuration | [View Activity](./atividade-2.3-criacao-alerta/) |
| 2.4 | Monitoring Dashboard | [View Activity](./atividade-2.4-dashboard/) |
| 2.5 | Security Monitoring Use Cases | [View Activity](./atividade-2.5-casos-uso-seguranca/) |

## Environment

| Component | Details |
|---|---|
| Virtual Machine | forenseLinux |
| Host Address | 192.168.98.10 |
| Splunk Version | 9.0.3 |
| Web Interface | Port 8000 |
| Log Source | /var/log/auth.log |
| Sourcetype | linux_secure |
| Main Interface | Search & Reporting |

## Tools and Technologies

| Category | Technology | Application |
|---|---|---|
| SIEM | Splunk Enterprise | Security event monitoring |
| Log Collection | Linux auth.log | Authentication and account activity |
| Search Language | SPL | Event filtering and field selection |
| Alerting | Real-time Alerts | Monitor events as they occur |
| Dashboards | Splunk Dashboards | Centralized event visualization |
| Linux Administration | useradd, passwd, gpasswd, sudo | Generate and inspect account events |

## Observed Monitoring Events

The available activity transcription records user creation and account-management events involving:

- `exemplo`
- `exemplo2`

Recorded Linux processes include:

- groupadd
- useradd
- passwd
- chfn
- gpasswd
- sudo

## Evidence

The original report uses five screenshots to document the practical activities.

[View Universal Class Evidence PDF](./evidences.pdf)

The same evidence document is referenced by all five activity READMEs.

## Technical Notes

An initial search encountered a Splunk license-related error. Subsequent activity records show successful event retrieval.

The alert configuration screenshot displayed no fired events, even though the report described a subsequent test involving `exemplo2`. Both observations are preserved in Activity 2.3.

The final SPL search returned 17 events within the selected 24-hour period.

## Learning Outcomes

- SIEM administration and access
- Linux authentication log analysis
- SPL search syntax
- User creation and account monitoring
- Real-time alert configuration
- Trigger condition interpretation
- Dashboard creation
- Root activity investigation
- Security monitoring and event correlation

## References

- [Splunk Enterprise Documentation](https://help.splunk.com/en/splunk-enterprise)
- [Splunk Search Reference](https://help.splunk.com/en/splunk-enterprise/search/spl-search-reference)
- [Splunk Real-Time Alerts](https://help.splunk.com/en/splunk-enterprise/alert-and-respond/alerting-manual/create-alerts/create-real-time-alerts)
- [Splunk Dashboard Studio](https://help.splunk.com/en/splunk-enterprise/create-dashboards-and-reports/dashboard-studio)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
