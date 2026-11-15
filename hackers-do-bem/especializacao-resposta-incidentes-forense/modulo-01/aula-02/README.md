# Hackers do Bem — Specialization | Module 01 — Class 02

Documentation of the practical activities from Class 02 of the Hackers do Bem Incident Response and Digital Forensics specialization.

This class explores security monitoring and incident investigation using Splunk Enterprise, including Linux authentication logs, alert configuration, dashboards, and security use cases.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 02 |
| Activities | 5 |
| Environment | forenseLinux VM |
| SIEM Platform | Splunk Enterprise 9.0.3 |

## Practical Activities

| Activity | Topic | Documentation |
|---|---|---|
| 2.1 | Splunk Enterprise | [View Activity](./atividade-2.1-splunk-enterprise/) |
| 2.2 | Authentication Log Monitoring | [View Activity](./atividade-2.2-monitoramento-logs/) |
| 2.3 | Alert Configuration | [View Activity](./atividade-2.3-criacao-alerta/) |
| 2.4 | Monitoring Dashboard | [View Activity](./atividade-2.4-dashboard/) |
| 2.5 | Security Monitoring Use Cases | [View Activity](./atividade-2.5-casos-uso-seguranca/) |

## Environment and Data Sources

| Component | Details |
|---|---|
| Virtual Machine | forenseLinux |
| Host | 192.168.98.10 |
| Splunk Version | 9.0.3 |
| Log Source | /var/log/auth.log |
| Sourcetype | linux_secure |
| Interface | Splunk Web |

## Skills Practiced

- Security information and event monitoring (SIEM)
- Linux authentication log analysis
- User account activity monitoring
- Alert configuration and event detection
- Dashboard creation and log visualization
- SPL search and filtering
- Privileged activity investigation
- Security monitoring use cases

## Documentation and Evidence

The class evidence PDF contains the practical screenshots associated with the five activities.

[View Class Evidence PDF](./evidences.pdf)

The written activity documentation was reconstructed from the available report and screenshot transcription. Technical findings and documented observations are distinguished from information that could not be independently verified.

## Technical Notes

- An expired-license message was recorded during an initial Splunk search.
- The alert configuration screenshot showed no fired events at the time of capture, although the report describes a subsequent alert trigger.
- The exact SPL query and results available from the activity transcription are documented in the corresponding activity README.

---

[Back to Specialization](../../README.md) · [Back to Hackers do Bem](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
