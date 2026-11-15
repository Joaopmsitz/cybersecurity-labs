# Hackers do Bem — Specialization | Module 01 — Class 03

Documentation of the practical activities from Class 03 of the Hackers do Bem Incident Response and Digital Forensics specialization.

This class explores network security monitoring, malware investigation, file analysis, automated file extraction, and incident response using Zeek.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 03 |
| Activities | 5 |
| Environment | forenseLinux VM |
| Primary Tool | Zeek |
| Focus | Malware and Email Incident Response |

## Practical Activities

| Activity | Topic | Documentation |
|---|---|---|
| 3.1 | Configuring Zeek | [View Activity](./atividade-3.1-configurando-zeek/) |
| 3.2 | File Analysis with Zeek | [View Activity](./atividade-3.2-analise-arquivos-zeek/) |
| 3.3 | Understanding Zeek Logs and JSON | [View Activity](./atividade-3.3-logs-json-zeek/) |
| 3.4 | Automatic File Extraction | [View Activity](./atividade-3.4-extracao-automatica-arquivos/) |
| 3.5 | Malware Investigation Use Case | [View Activity](./atividade-3.5-caso-uso-malware-email/) |

## Tools and Technologies

| Category | Tools | Context |
|---|---|---|
| Network Security Monitoring | Zeek | Network traffic analysis and security monitoring |
| File Analysis | Zeek File Analysis Framework | File identification and metadata analysis |
| Cryptographic Hashing | MD5, SHA1, SHA256 | File identification and integrity analysis |
| Malware Intelligence | Team Cymru Malware Hash Registry | Known malware hash matching |
| Network Analysis | conn.log, dns.log, http.log | Network activity investigation |
| File Extraction | Zeek File Extraction Framework | Automatic extraction of transferred files |
| Log Processing | Zeek JSON Logs | Structured security event analysis |

## Evidence Requirements

The original practical assignment requires one PDF containing the five requested screenshots.

| Activity | Required Screenshot |
|---|---|
| 3.1 | Step 2 |
| 3.2 | Step 2 |
| 3.3 | Step 5 |
| 3.4 | Step 6 |
| 3.5 | Step 1 |

[View Universal Class Evidence PDF](./evidences.pdf)

The same evidence document is referenced by all five activity READMEs.

## Learning Outcomes

- Zeek service configuration and deployment
- Network security monitoring
- File hashing and SHA256 analysis
- Malware hash intelligence
- Structured JSON log generation
- Automatic file extraction
- Network traffic investigation
- Correlation of security events
- Identification and documentation of indicators of compromise

## Technical Notes

The final activity uses a historical training scenario involving a suspicious executable delivered through a download link associated with a supposed employee bonus.

The scenario demonstrates how Zeek logs can support incident investigation through connection identifiers, file identifiers, hashes, network addresses, and malware intelligence.

The example indicators are presented as training material and are not represented as current threat intelligence.

## References

- [Official Zeek Documentation](https://docs.zeek.org/en/master/)
- [Zeek — About](https://docs.zeek.org/en/master/about.html)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Hackers do Bem](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
