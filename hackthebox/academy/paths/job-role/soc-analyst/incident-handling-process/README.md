# Incident Handling Process

> HTB Academy — SOC Analyst Job Role Path (CDSA)

## Overview

This module covers the incident handling lifecycle, investigation, detection and analysis, response, recovery, and post-incident activities.

---

## Incident Handling Lifecycle

```text
Preparation
     ↓
Detection & Analysis
     ↓
Containment, Eradication & Recovery
     ↓
Post-Incident Activity
     ↺
```

Incident handling is a continuous process that evolves as new evidence and leads are identified.

---

## Core Concepts

### Cyber Kill Chain

```text
Reconnaissance → Weaponization → Delivery → Exploitation
→ Installation → Command & Control → Actions on Objectives
```

The goal of defenders is to detect and disrupt adversary activity as early as possible.

### MITRE ATT&CK

MITRE ATT&CK provides a structured way to describe adversary behavior through tactics, techniques, and sub-techniques.

| Technique | Description                         |
| --------- | ----------------------------------- |
| T1059.001 | PowerShell                          |
| T1021.001 | Remote Services: RDP                |
| T1003.001 | OS Credential Dumping: LSASS Memory |
| T1105     | Ingress Tool Transfer               |
| T1555     | Credentials from Password Stores    |
| T1486     | Data Encrypted for Impact           |

### Pyramid of Pain

```text
             TTPs
           Tools
      Network/Host Artifacts
          Domains
            IPs
           Hashes
```

Hashes and IPs are easier to change, while tools and TTPs are more difficult to replace.

---

## Investigation Process

### Detection & Analysis

Detection can originate from:

* User reports
* SIEM / EDR alerts
* Network security devices
* Threat hunting
* Third-party notifications

Effective detection requires visibility across network, endpoint, and application layers.

### Investigation Cycle

```text
Initial Investigation Data
          ↓
       IOCs
          ↓
New Leads & Affected Systems
          ↓
Collect & Analyze Data
          ↺
```

Investigation is iterative: new findings generate new leads, which guide further collection and analysis.

### Indicators of Compromise

Common IOCs include:

* IP addresses
* File hashes
* File names
* Domains
* Other host or network artifacts

IOC matches must be validated to reduce false positives and identify additional affected systems.

### Evidence Collection

* Minimize interaction with affected systems
* Preserve volatile evidence when necessary
* Use live response when appropriate
* Maintain chain of custody when required
* Understand how investigative tools affect evidence and credentials

### Incident Timeline

A timeline helps correlate evidence and reconstruct attacker activity.

| Date | Time | Host | Event | Source |
| ---- | ---- | ---- | ----- | ------ |

### Severity & Communication

Severity should consider impact, scope, affected systems, business criticality, propagation, and available remediation.

Incident information should follow a **need-to-know** principle and use controlled communication channels.

---

## Incident Response

### Preparation

Incident response capability should be established before an incident occurs.

Key areas:

* Response policies and procedures
* Roles and escalation paths
* Asset inventory and network documentation
* Known-clean baselines
* Evidence preservation
* Secure communication
* Forensic resources

### Protective Controls

* Endpoint and identity hardening
* MFA and privileged access controls
* Network segmentation and monitoring
* Vulnerability management
* Security awareness

### Containment, Eradication & Recovery

```text
Containment
     ↓
Eradication
     ↓
Recovery
     ↓
Validation
```

Contain affected systems, remove malicious activity and persistence, restore operations, and validate the environment.

---

## Tools & Technologies

| Tool         | Purpose                                |
| ------------ | -------------------------------------- |
| TheHive      | Incident and case management           |
| Wazuh / SIEM | Alerting, monitoring, and log analysis |
| Sysmon       | Windows telemetry                      |
| EDR          | Endpoint visibility and detection      |
| MITRE ATT&CK | Adversary behavior mapping             |

Practical exercises from this module are documented separately under `labs/`.

---

## Investigation Workflow

```text
Detection
   ↓
Initial Triage
   ↓
Establish Context
   ↓
Determine Scope
   ↓
Identify IOCs / TTPs
   ↓
Build Timeline
   ↓
Collect & Analyze Evidence
   ↓
Containment
   ↓
Eradication
   ↓
Recovery
   ↓
Lessons Learned
```

---

## Key Takeaways

* Incident response begins before an incident occurs.
* Investigation is an iterative process driven by evidence and new leads.
* IOC matches must be validated to avoid false positives.
* Timelines help reconstruct attacker activity.
* Live response can preserve volatile evidence.
* Chain of custody helps maintain evidence integrity.
* MITRE ATT&CK provides a structured language for adversary behavior.
* Effective preparation, visibility, and detection directly improve incident response.

---

## References

* Hack The Box Academy — Incident Handling Process
* MITRE ATT&CK
* NIST SP 800-61
