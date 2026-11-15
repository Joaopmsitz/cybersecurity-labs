# Hackers do Bem — Specialization | Module 01 — Class 05

This class examines the infrastructure, technologies, processes, and operational capabilities required to establish a Computer Security Incident Response Team (CSIRT). The activities analyze basic and virtualized architectures, enterprise network monitoring, incident response workflows, and the services required to support incident handling.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 05 |
| Activities | 5 |
| Main Topics | CSIRT Infrastructure, High Availability, Virtualization, Storage Area Networks, Enterprise Network Security, Incident Management, Communication, and Business Continuity |

## Practical Activities

| Activity | Topic | Description | Documentation |
| -------- | ----- | ----------- | ------------- |
| 5.1 — Analyzing a Basic CSIRT Infrastructure | Infrastructure Analysis | Evaluate connectivity redundancy, high availability, and laboratory isolation in a basic CSIRT architecture. | [View Activity](./atividade-5.1-simple-csirt-infrastructure/README.md) |
| 5.2 — Analyzing a Virtualized CSIRT Infrastructure | Virtualization and Storage | Analyze virtual machine clusters, SAN dependencies, resource utilization, and infrastructure availability. | [View Activity](./atividade-5.2-virtualized-csirt-infrastructure/README.md) |
| 5.3 — Analyzing an Enterprise-Scale Network Architecture | Network Security | Evaluate network segmentation, traffic monitoring, defense in depth, and enterprise infrastructure dependencies. | [View Activity](./atividade-5.3-enterprise-network-architecture/README.md) |
| 5.4 — Analyzing an Incident Response Workflow | Incident Management | Analyze incident triage, ticket queues, investigation workflows, and lessons learned. | [View Activity](./atividade-5.4-incident-response-workflow/README.md) |
| 5.5 — Discussion of Incident Handling Infrastructure and Services | CSIRT Operations | Discuss incident reporting, ticketing, communication, monitoring, continuity, remote access, and investigation tools. | [View Activity](./atividade-5.5-incident-handling-service-discussion/README.md) |

## Environment

This class is primarily based on infrastructure diagrams, architecture comparisons, and written analysis of incident response operations.

The software and technologies discussed in the activities are examples of possible CSIRT solutions. They should not be interpreted as products installed or deployed during the exercises.

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Incident Management | RTIR, Ticketing Systems | Organize incident reports, ownership, prioritization, and response workflows. |
| Threat Intelligence | MISP | Manage and share indicators of compromise. |
| Availability Monitoring | Zabbix, Nagios, PRTG | Monitor servers, network devices, connectivity, and service availability. |
| Network Security | Firewalls, IDS, Aggregation TAP | Protect network segments and provide traffic visibility. |
| Forensic Analysis | Wireshark, Autopsy | Inspect network traffic and perform digital forensic examinations. |
| Secure Remote Access | VPN, SSH | Enable authenticated and encrypted remote access for analysts. |
| Infrastructure | HA Clusters, Virtualization, SAN | Support service availability, resource consolidation, and centralized storage. |

## Learning Outcomes

- Identify the components required for a basic CSIRT infrastructure.
- Evaluate redundancy, high availability, and laboratory isolation.
- Understand virtualization and centralized storage dependencies.
- Analyze enterprise network segmentation and monitoring architectures.
- Understand incident triage and ticket-based response workflows.
- Identify communication and incident reporting requirements.
- Evaluate network monitoring, business continuity, and remote investigation capabilities.
- Select appropriate technologies for incident handling operations.

## Evidence Requirements

The original practical assignment consolidates the required evidence into a single PDF document.

[View Universal Class Evidence PDF](./evidences.pdf)

The universal evidence PDF contains the written analyses for Activities 5.1 through 5.5, including the ten discussion questions in Activity 5.5.

## Technical Notes

- The activity compares proposed architectures and operational processes. The assessment of strengths and weaknesses is based on the diagrams and scenarios supplied in the course.
- RTIR, MISP, Zabbix, Nagios, PRTG, Wireshark, and Autopsy are discussed as possible tools. Their mention does not mean that they were installed or deployed during the activities.
- A centralized SAN can improve storage management and support virtualized workloads, but its availability and connectivity must be considered when evaluating infrastructure dependencies.

## References

- ENISA (2016). Developing CSIRT Infrastructure 1.0. European Union Agency for Network and Information Security.
- [NIST SP 800-61 Rev. 3 — Incident Response Recommendations](https://csrc.nist.gov/pubs/sp/800/61/r3/final)
- [NIST — Revision 3 Announcement](https://www.nist.gov/news-events/news/2025/04/nist-revises-sp-800-61-incident-response-recommendations-and-considerations)
- [Security Onion Documentation](https://docs.securityonion.net/en/3/dev/introduction/)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
