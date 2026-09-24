# 🎯 FortySeven-1 — Sherlock (Very Easy)

🔗 Completion Proof:  
[Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/1200)

## 📝 Description

FortySeven-1 is a Threat Intelligence-focused Sherlock centered on profiling an Advanced Persistent Threat (APT) group through the analysis of multiple public intelligence reports.

The challenge investigates **Mysterious Elephant (APT-K-47)**, a threat actor linked to phishing campaigns targeting government and diplomatic personnel. The objective was to correlate intelligence from different sources to identify the group's tools, infrastructure, attack techniques, persistence mechanisms, and operational objectives.

## ✔ Skills Practiced

- Threat Intelligence Analysis
- APT Profiling
- Open-Source Intelligence (OSINT)
- Intelligence Correlation
- Threat Actor Attribution
- MITRE ATT&CK Mapping
- Malware Family Analysis
- Campaign Tracking
- TTP Analysis
- Strategic Threat Research

## 🛠 Tools Used

- Public Threat Intelligence Reports
- Kaspersky Securelist Research
- Knownsec 404 Research
- MITRE ATT&CK Framework
- OSINT Sources
- Manual Intelligence Correlation

## 🔎 Key Findings

During the investigation, it was possible to identify:

- The threat actor known as **Mysterious Elephant (APT-K-47)**
- Attack activity dating back to 2022
- The use of ORPCBackdoor malware
- The AsyncShell malware family
- WhatsApp-focused data collection operations
- Hajj-themed phishing campaigns
- DLL side-loading techniques
- Hidden desktop execution methods
- Sandbox evasion mechanisms
- Custom persistence mechanisms
- Custom exfiltration tools
- Command-and-control communications over HTTP and HTTPS

The investigation required correlating multiple intelligence reports to build a complete profile of the actor, including its malware ecosystem, attack methodologies, and operational objectives.

## 🧠 MITRE ATT&CK

- T1566.001 — Spearphishing Attachment
- T1190 — Exploit Public-Facing Application
- T1059 — Command and Scripting Interpreter
- T1059.001 — PowerShell
- T1218 — System Binary Proxy Execution
- T1053 — Scheduled Task
- T1547.001 — Registry Run Keys / Startup Folder
- T1574.002 — DLL Side-Loading
- T1027 — Obfuscated Files or Information
- T1497 — Virtualization/Sandbox Evasion
- T1082 — System Information Discovery
- T1057 — Process Discovery
- T1071 — Application Layer Protocol
- T1105 — Ingress Tool Transfer
- T1041 — Exfiltration Over C2 Channel

## 📚 Knowledge Gained

- Threat Intelligence fundamentals
- APT attribution methodologies
- Threat actor profiling
- Intelligence report correlation
- MITRE ATT&CK analysis
- Malware ecosystem research
- Campaign tracking techniques
- Adversary TTP identification

---

# 🔍 HTB Sherlocks — Threat Intelligence & APT Investigations

Hack The Box Sherlocks focus on:

- Threat Intelligence
- Digital Forensics
- Incident Response
- Malware Analysis
- Threat Hunting
- IOC Analysis
- Threat Actor Profiling
- Security Investigations

These challenges simulate real-world scenarios where analysts must gather and correlate information from multiple sources, understand attacker behavior, identify operational objectives, and validate intelligence using industry-standard methodologies.
