# 🎯 FortySeven-1 — Sherlock (Very Easy)

🔗 Completion Proof:  
[Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/1200)

## 📝 Description

FortySeven-1 is a Threat Intelligence-focused Sherlock that simulates the investigation of an Advanced Persistent Threat (APT) campaign targeting government and diplomatic officials.

The challenge required correlating intelligence from multiple security vendor reports in order to build a profile of the threat actor known as **Mysterious Elephant (APT-K-47)**. The investigation focused on attribution, malware families, phishing campaigns, persistence mechanisms, exfiltration methods, and MITRE ATT&CK techniques.

## ✔ Skills Practiced

- Threat Intelligence Analysis
- APT Profiling
- Open-Source Intelligence (OSINT)
- Intelligence Correlation
- MITRE ATT&CK Mapping
- Threat Actor Attribution
- Malware Family Analysis
- Campaign Tracking
- Threat Research
- TTP Analysis

## 🛠 Tools Used

- Security Vendor Reports
- Kaspersky Securelist
- Knownsec 404 Research
- MITRE ATT&CK Framework
- Open-Source Intelligence (OSINT)
- Manual Research & Correlation

## 🔎 Key Findings

During the investigation it was possible to identify:

- The threat actor known as **Mysterious Elephant (APT-K-47)**
- Attack activity dating back to 2022
- The use of ORPCBackdoor malware
- The AsyncShell malware family
- WhatsApp-targeted data theft operations
- Hajj-themed phishing campaigns
- DLL side-loading techniques
- Hidden desktop execution methods
- Sandbox evasion mechanisms
- Multiple persistence techniques
- Custom exfiltration tools
- Command-and-control communication over HTTP and HTTPS

The investigation required correlating multiple public threat intelligence reports in order to identify the actor's infrastructure, tools, operational objectives, and attack methodology.

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

These challenges simulate real-world scenarios where analysts must collect information from multiple sources, identify attacker behavior, understand operational objectives, and validate intelligence using industry-standard methodologies.
