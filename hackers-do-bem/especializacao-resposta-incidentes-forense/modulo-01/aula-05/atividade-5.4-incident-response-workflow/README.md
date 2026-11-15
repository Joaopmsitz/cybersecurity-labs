# Activity 5.4 — Analyzing an Incident Response Workflow

## Objective

Analyze the incident management workflow presented in the course material.

The workflow describes how a report becomes a ticket, how the report is classified, and how the ticket is routed through different queues depending on whether it represents a security incident and whether the incident has already been analyzed.

The activity requires identifying and explaining at least one strength and one weakness of the proposed process.

## Workflow overview

The process contains the following main stages:

1. A new ticket is created from a received report.
2. The report is evaluated to determine whether it is related to a security incident.
3. Security incidents are directed to the IncidentQueue. Other reports are sent to the MiscQueue.
4. The designated owner determines whether the incident is already known, recently resolved, or new.
5. New incidents are sent to the AnalysisQueue.
6. Once the analysis is completed, the ticket returns to the IncidentQueue.
7. Cases requiring post-incident review are sent to the LessonsLearnedQueue, where the investigation and countermeasures are documented in the knowledge base.

## Analysis

### Strength — Efficient triage and knowledge generation

The initial triage stage separates genuine security incidents from other types of requests.

This improves the use of the CSIRT's resources because reports that do not represent security incidents can be handled separately instead of consuming the time of incident response analysts.

The workflow also includes a LessonsLearnedQueue.

This stage allows the team to document incident analysis, response actions, and countermeasures. The information can then be incorporated into a knowledge base and used to improve future investigations.

A structured process for triage and lessons learned supports consistency, traceability, and continuous improvement.

### Weakness — Potential delays and rework

The workflow allows tickets to move between the AnalysisQueue and IncidentQueue.

This movement is part of the intended process, but it may create delays or repeated work when incidents are complex, documentation is incomplete, or the criteria for transferring tickets between queues are not clear.

Another weakness is the absence of an explicitly defined immediate escalation path for critical incidents in the described workflow.

A severe incident may require rapid decisions, coordination with management, and immediate containment actions. Without clear escalation criteria, the response could be delayed.

Possible improvements include:

- Define severity levels and prioritization criteria.
- Establish response and escalation SLAs.
- Create an immediate escalation path for critical incidents.
- Standardize the information required before transferring a ticket.
- Assign clear ownership at each workflow stage.
- Record decisions, analysis, and response actions in the ticket.
- Automate notifications and escalation for overdue critical cases.
- Maintain metrics for triage time, analysis time, and incident resolution.

## Technical assessment

The separation of work into dedicated queues helps organize the response process and makes ticket ownership more visible.

However, a queue-based process must be supported by clear responsibilities, prioritization, escalation rules, and complete documentation. Otherwise, tickets may remain in queues for too long or be repeatedly transferred without meaningful progress.

The LessonsLearnedQueue is particularly valuable because it turns individual incident investigations into reusable organizational knowledge.

## Conclusion

The main strength is the use of an initial triage process combined with a dedicated lessons-learned stage.

The main weakness is the possibility of delays and rework during ticket transfers, especially when incidents are poorly documented or when critical cases do not have a clearly defined escalation path.

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)
