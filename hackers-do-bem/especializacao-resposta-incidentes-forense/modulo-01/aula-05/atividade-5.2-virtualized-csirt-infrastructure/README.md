# Activity 5.2 — Analyzing a Virtualized CSIRT Infrastructure

## Objective

Analyze an updated CSIRT infrastructure that incorporates virtualization, a Storage Area Network (SAN), and Voice over IP (VoIP).

The course material presents an architecture in which different services are organized into frontend, services, data/storage, and network layers.

The exercise requires identifying and explaining at least one strength and one weakness of the proposed solution.

## Analysis

### Strength — Resource efficiency and logical isolation

The use of a Virtual Machine Cluster connected to a SAN allows multiple servers and services to run on a centralized physical infrastructure.

Examples of the services represented in the proposed environment include:

- Office services.
- Web services.
- Incident handling systems.
- Forensic analysis systems.
- Data and storage services.
- Network and communication components.

Virtualization improves resource utilization because multiple workloads can share physical computing resources instead of requiring a separate physical server for every service.

It also provides flexibility for provisioning, managing, and relocating virtual machines.

Logical separation between virtual machines and network segments can improve isolation between services and reduce the impact of failures or compromises affecting a specific system.

A virtualized environment can also support recovery operations through snapshots, templates, replication, and migration, provided these capabilities are properly configured.

### Weakness — SAN dependency and increased complexity

Although virtualization can improve availability and resource efficiency, dependence on a centralized SAN creates an important infrastructure dependency.

If the SAN, its controllers, or its connectivity become unavailable, multiple virtualized services may be affected simultaneously.

This can create a significant operational risk when the CSIRT depends on the same storage infrastructure for incident handling, forensic analysis, and other critical functions.

The architecture also introduces additional management and troubleshooting complexity.

Storage performance and network capacity must be planned carefully, particularly when forensic investigations, packet capture, and other data-intensive activities occur simultaneously.

Depending on the SAN architecture, storage and service traffic may also compete for shared physical resources, potentially creating bottlenecks.

Possible mitigations include:

- Redundant storage controllers.
- Multiple independent storage paths.
- Multipath configuration.
- Redundant network switches and links.
- Capacity and performance monitoring.
- Separate network paths for storage and ordinary service traffic when appropriate.
- Tested backup and disaster recovery procedures.
- Documented recovery priorities for critical CSIRT services.

## Technical assessment

Virtualization provides flexibility and reduces the need for dedicated physical servers. It also makes it easier to organize services into logical environments.

However, virtualization does not automatically guarantee high availability. The physical infrastructure underneath the virtual machines, particularly storage, networking, power, and hypervisor management, must also be redundant and monitored.

The SAN should not become an unprotected single point of failure.

## Conclusion

The main strength is the efficient use of computing resources and the logical separation of services through virtualization.

The main weakness is the dependence on centralized storage and the additional complexity of managing the virtualized infrastructure. Redundant storage paths, independent network components, and tested recovery procedures are essential to reduce these risks.

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)
