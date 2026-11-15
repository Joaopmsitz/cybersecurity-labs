# Activity 5.1 — Analyzing a Basic CSIRT Infrastructure

## Objective

Analyze the basic infrastructure proposed for a team dedicated to incident response. Identify and explain at least one strength and one weakness of the proposed solution.

The course material describes a basic environment containing the essential elements of a CSIRT, including laboratory resources, communication, incident management, and incident response capabilities.

## Analysis

### Strength — Redundant connectivity and high availability

The infrastructure has two Internet connections, consisting of a primary link and a backup link.

This redundancy improves service availability and reduces the risk of the CSIRT becoming isolated if one Internet service provider experiences an outage.

The use of a high-availability cluster for incident handling servers also contributes to operational continuity. If one server becomes unavailable, the cluster can help maintain the availability of the services handled by the remaining infrastructure, depending on its configuration.

These mechanisms are important because the CSIRT depends on reliable communication and incident management resources, particularly during security events that affect the organization's connectivity.

### Weakness — Insufficient segmentation and isolation of the laboratory

Although the infrastructure includes a DMZ for Web and Mail servers, the laboratory subnet appears to remain connected to the main network through the firewall.

This arrangement can represent a security risk because malware analysis and other forensic activities may involve suspicious files, compromised systems, and potentially dangerous network behavior.

If the laboratory is not sufficiently isolated, malicious activity could reach production systems or other components used by the CSIRT.

A malware analysis environment should therefore use strict logical or physical isolation, depending on the risk. Possible controls include:

- Dedicated laboratory network segments.
- Strict firewall rules between the laboratory and production networks.
- Controlled access to external networks.
- Restricted transfer of files between isolated and trusted environments.
- Disposable virtual machines and snapshots for analysis.
- Monitoring of laboratory traffic.
- A dedicated analysis environment for samples that require stronger isolation.

For high-risk malware analysis, an air-gapped environment may be appropriate.

## Technical assessment

The proposed infrastructure establishes a useful foundation for a new incident response team because it considers connectivity redundancy and server availability.

However, availability alone is not sufficient. The CSIRT must also protect its own investigation environment. Laboratory segmentation is particularly important because malware analysis can expose the organization to additional risks if suspicious systems are connected to production networks without appropriate controls.

## Conclusion

The main strength is the combination of redundant Internet connectivity and high-availability incident handling servers.

The main weakness is the apparent lack of strict isolation between the laboratory subnet and the main network. Improving network segmentation and controlling communication between environments would reduce the risk of malware propagation.

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)
