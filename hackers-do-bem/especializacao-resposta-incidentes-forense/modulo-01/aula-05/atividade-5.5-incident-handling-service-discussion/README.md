# Activity 5.5 — Discussion of Incident Handling Infrastructure and Services

## Objective

Discuss the infrastructure, tools, communication channels, and operational practices required to provide incident handling services.

The exercise contains ten questions about incident reporting, teamwork, response workflows, report storage, availability, monitoring, network failures, infrastructure protection, remote work, and software required for incident analysis.

The answers below document the responses submitted for the activity.

---

## Question 1

**Question:** Incidents can be reported through several channels. Which channels should CSIRT teams maintain at a minimum?

**Answer:**

At a minimum, a CSIRT should maintain a dedicated incident-reporting email address, preferably with support for PGP/GPG encryption, as well as a structured web form for collecting incident information.

A telephone channel should also be available for critical incidents that require immediate response.

These channels provide different ways for users and external organizations to report security events. The CSIRT should define procedures for monitoring, prioritizing, and handling reports received through each channel.

## Question 2

**Question:** Which tools can be used to better organize teamwork and the flow of information, especially for incidents reported through the Internet?

**Answer:**

Ticketing tools such as RTIR or similar incident management systems can be used to track reports, assign responsibilities, document investigation steps, and organize the workflow of the response team.

Threat Intelligence platforms such as MISP can complement this process by supporting the management and sharing of indicators of compromise received from external sources.

Together, these tools help maintain traceability, improve information sharing, and organize the investigation process.

## Question 3

**Question:** How should we organize the incident response process? Use Figure 5 — Incident Response Workflow.

**Answer:**

The incident response process should follow a structured workflow.

First, a new ticket is created from the received report. The report then passes through an initial triage stage to determine whether it represents a genuine security incident.

If the report is not related to a security incident, it is sent to the MiscQueue. If it is a security incident, it is directed to the IncidentQueue.

The designated owner then determines whether the incident is already known, recently resolved, or new:

1. If the incident has already been analyzed and resolved, the ticket can be closed.
2. If it was recently resolved but still requires a lessons-learned review, it is sent to the LessonsLearnedQueue.
3. If it is a new incident, it is sent to the AnalysisQueue for technical investigation.

After the analysis is completed, the ticket returns to the IncidentQueue for the appropriate response actions.

The LessonsLearnedQueue is responsible for documenting the incident, its analysis, and the countermeasures applied, incorporating the information into the organization's knowledge base.

This process provides structured triage, investigation, response, and continuous improvement.

## Question 4

**Question:** Where should incident reports be stored, and why is this so important?

**Answer:**

Incident reports should be stored in centralized, secure, and encrypted repositories or databases with controlled access.

This is important because reports may contain sensitive information, technical evidence, indicators of compromise, and details about affected systems.

Centralized storage helps preserve the incident history, support audits, maintain investigation traceability, and allow future analysis of attack trends and recurring patterns.

Access controls, backups, retention policies, and integrity protections should be applied to prevent unauthorized access or loss of information.

## Question 5

**Question:** How can we prevent failures or unavailability of communication channels and servers?

**Answer:**

The risk of unavailability can be reduced through high-availability servers, redundant Internet connections, periodic backups, and business continuity procedures.

High-availability clusters can help maintain the operation of critical services when a server fails. Redundant connectivity can preserve access to external communication channels if the primary Internet link becomes unavailable.

The organization should also test its backup and recovery procedures regularly and maintain contingency plans for communication and incident management.

## Question 6

**Question:** How can we monitor our network for failures or unavailability of servers, Internet connections, and other services?

**Answer:**

Monitoring platforms such as Zabbix, Nagios, and PRTG can be used to identify network failures, unavailable services, and connectivity problems.

These tools can monitor servers, network devices, links, and applications, generating alerts when availability or performance thresholds are violated.

Intrusion Detection Systems can complement infrastructure monitoring by identifying network anomalies and suspicious activity.

Availability monitoring and security monitoring should work together, but they serve different purposes: infrastructure monitoring focuses on operational health, while IDS technologies focus on detecting suspicious or potentially malicious behavior.

## Question 7

**Question:** How should we respond to network failures?

**Answer:**

Network failures should be detected quickly and handled according to the organization's Business Continuity Plan (BCP).

The response team should identify the affected components, determine the operational impact, and activate the appropriate contingency procedures.

In critical situations, traffic can be redirected to backup Internet links or redundant network equipment to maintain essential services.

The incident should be documented, stakeholders should be informed, and the failed components should be investigated and restored as soon as possible.

## Question 8

**Question:** How should we protect all CSIRT infrastructure?

**Answer:**

CSIRT infrastructure should be protected through a defense-in-depth strategy.

Important controls include:

- Firewalls and network segmentation.
- Multifactor authentication (MFA).
- Encryption of sensitive data in transit and at rest.
- Role-based access control and least privilege.
- Regular security updates and vulnerability management.
- Endpoint protection and security monitoring.
- Secure backups and recovery procedures.
- Centralized logging and access auditing.
- Physical protection of servers and network equipment.

These controls reduce the likelihood of unauthorized access and help contain the impact of a compromise.

## Question 9

**Question:** Incident analysis sometimes requires working outside the network center or laboratory. Which tools are useful for remote work?

**Answer:**

Secure VPN connections, SSH, protected corporate laptops, and authenticated remote access tools are useful for remote incident analysis.

These technologies allow analysts to access authorized systems and investigate incidents without being physically present in the organization's network center or laboratory.

Remote access must be protected with strong authentication, encryption, access restrictions, and monitoring.

Administrative services should not be exposed directly to the Internet without appropriate security controls.

## Question 10

**Question:** What basic software is necessary to perform incident analysis?

**Answer:**

Incident analysis requires tools that support different stages of investigation.

Examples include:

- **Wireshark:** Network traffic capture and protocol analysis.
- **Autopsy:** Digital forensic examination of storage devices and file systems.
- **Log analysis and SIEM platforms:** Collection, correlation, and investigation of security events.
- **Antivirus and endpoint detection tools:** Identification and investigation of malicious files and behavior.
- **Hexadecimal editors:** Inspection and modification of binary data.
- **Debuggers:** Analysis of program execution and suspicious software behavior.
- **Kali Linux:** A security-oriented Linux distribution that provides access to various assessment and investigation utilities.

The exact toolset depends on the CSIRT's responsibilities, the environment being investigated, and the type of incident.

## Technical conclusion

The discussion demonstrates that an effective CSIRT requires more than technical analysis tools. It also depends on reliable communication, organized incident management, secure information storage, availability monitoring, network redundancy, and documented response procedures.

A well-structured CSIRT combines people, processes, and technology to receive reports, investigate incidents, coordinate response actions, preserve evidence, and improve its capabilities through lessons learned.

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

## Reference

ENISA (2016). *Developing CSIRT Infrastructure 1.0*. European Union Agency for Network and Information Security.
