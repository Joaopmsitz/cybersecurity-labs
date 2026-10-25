# FortySeven-1 — Sherlock (Very Easy)

**Category:** Threat Intelligence  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/1200)

## Overview

FortySeven-1 is a Sherlock challenge focused on threat intelligence and Advanced Persistent Threat (APT) profiling.

The investigation involved correlating public reports from multiple security vendors to build a profile of **Mysterious Elephant (APT-K-47)**, examining its malware, phishing campaigns, persistence techniques, exfiltration methods, and operational behavior.

## Investigation Focus

- Threat intelligence research and correlation
- APT profiling and threat actor attribution
- Open-Source Intelligence (OSINT)
- Malware family identification
- Phishing campaign analysis
- Adversary tactics, techniques, and procedures (TTPs)
- Command-and-control and data exfiltration methods
- MITRE ATT&CK mapping

## Sources and Tools

- Kaspersky Securelist reports
- Knownsec 404 Research
- MITRE ATT&CK Framework
- Public threat intelligence reports
- Manual research and intelligence correlation

## Key Findings

The investigation identified or examined:

- Mysterious Elephant (APT-K-47) as the threat actor associated with the campaign
- Reported activity dating back to 2022
- ORPCBackdoor and AsyncShell malware families
- WhatsApp-focused data collection operations
- Hajj-themed phishing campaigns
- DLL side-loading and hidden desktop execution techniques
- Sandbox-evasion and persistence mechanisms
- Custom data-exfiltration tools
- Command-and-control communications over HTTP and HTTPS

Correlating multiple intelligence reports helped connect the actor's tools, infrastructure, techniques, and operational objectives.

## MITRE ATT&CK

The following techniques were identified in the intelligence reviewed during the investigation:

- **T1566.001** — Spearphishing Attachment
- **T1190** — Exploit Public-Facing Application
- **T1059** — Command and Scripting Interpreter
- **T1059.001** — PowerShell
- **T1218** — System Binary Proxy Execution
- **T1053** — Scheduled Task/Job
- **T1547.001** — Registry Run Keys / Startup Folder
- **T1574.002** — DLL Side-Loading
- **T1027** — Obfuscated Files or Information
- **T1497** — Virtualization/Sandbox Evasion
- **T1082** — System Information Discovery
- **T1057** — Process Discovery
- **T1071** — Application Layer Protocol
- **T1105** — Ingress Tool Transfer
- **T1041** — Exfiltration Over C2 Channel

## Key Takeaways

- Threat actor profiling benefits from correlating multiple independent intelligence sources.
- Malware families and infrastructure can help connect related campaigns.
- MITRE ATT&CK provides a common framework for describing adversary behavior.
- OSINT supports analysis of threat actors, campaigns, and operational patterns.
- Intelligence assessments should distinguish reported facts from analytical conclusions.

---

[Back to Sherlocks](./README.md) · [Back to Hack The Box](../README.md)
