# Incident Handling Process

> HTB Academy — SOC Analyst Job Role Path (CDSA)

## Overview

This module covers the incident handling lifecycle, investigation, detection and analysis, containment, eradication, recovery, and post-incident activities.

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

Incident handling is a continuous process driven by new evidence, findings, and lessons learned.

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

Hashes and IPs are easier to change, while tools and TTPs are harder for adversaries to replace.

---

## Investigation Process

### Detection & Analysis

Detection can originate from:

* User reports
* SIEM / EDR alerts
* Network security controls
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

Investigation is iterative: new findings generate new leads and guide further collection and analysis.

### Indicators of Compromise

Common IOCs include:

* IP addresses
* File hashes
* File names
* Domains
* Host and network artifacts

IOC matches must be validated to reduce false positives and identify additional affected systems.

STIX and OpenIOC can be used to represent and exchange IOC information, while YARA can support pattern-based detection.

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

Severity should consider:

* Impact
* Scope
* Business-critical systems
* Number of affected systems
* Threat propagation
* Available remediation

Incident information should follow a **need-to-know** principle and use controlled communication channels.

---

## Incident Response

### Preparation

Incident response capability should be established before an incident occurs.

Key areas include:

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

### Containment

Containment aims to limit damage and prevent further spread.

**Short-term containment** focuses on rapid isolation while preserving evidence.

**Long-term containment** introduces persistent changes such as password resets, firewall rules, patches, and additional monitoring.

### Eradication

* Remove malware and persistence
* Rebuild or restore affected systems
* Apply required patches
* Harden affected systems and the wider environment

### Recovery

```text
Containment
     ↓
Eradication
     ↓
Recovery
     ↓
Validation
```

Restore normal operations, validate systems before returning them to production, and increase logging and monitoring after recovery.

---

## Post-Incident Activity

The post-incident stage focuses on improving future response capabilities.

* Conduct lessons-learned reviews
* Perform root cause analysis
* Update policies, playbooks, and detection rules
* Improve training, tooling, and readiness
* Document the incident and close the case

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

## Tools & Technologies

| Tool         | Purpose                                |
| ------------ | -------------------------------------- |
| TheHive      | Incident and case management           |
| Wazuh / SIEM | Alerting, monitoring, and log analysis |
| Sysmon       | Windows telemetry                      |
| EDR          | Endpoint visibility and detection      |
| MITRE ATT&CK | Adversary behavior mapping             |

---

## Key Takeaways

* Incident response begins before an incident occurs.
* Investigation is an iterative process driven by evidence and new leads.
* IOC matches must be validated to reduce false positives.
* Timelines help reconstruct attacker activity.
* Live response can preserve volatile evidence.
* Chain of custody helps maintain evidence integrity.
* MITRE ATT&CK provides a structured language for adversary behavior.
* Effective preparation, visibility, and detection improve incident response.

---

## References

* Hack The Box Academy — Incident Handling Process
* MITRE ATT&CK
* NIST SP 800-61
* OASIS STIX
