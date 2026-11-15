# Hackers do Bem — Specialization | Module 01 — Class 03

This class explores Zeek as a network security monitoring and investigation platform. The activities cover deployment, file hashing, structured JSON logging, automatic file extraction, and the investigation of suspicious downloads using network and file-related telemetry.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 03 |
| Activities | 5 |
| Main Topics | Network Security Monitoring, Zeek, File Analysis, Cryptographic Hashing, JSON Logs, File Extraction, and Malware Investigation |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|

## Environment

The activities used the `forenseLinux` environment with Zeek installed and configured for network traffic monitoring.

| Component | Details |
|---|---|
| Environment | forenseLinux |
| Zeek Installation | `/opt/zeek` |
| Network Interface | `ens5` |
| Current Logs | `/opt/zeek/logs/current/` |
| Configuration | `local.zeek` |
| Management Utility | ZeekControl |
| Package Manager | ZKG |

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Network Monitoring | Zeek | Inspect network activity and generate security telemetry. |
| Service Management | ZeekControl | Check, deploy, and manage the Zeek monitoring service. |
| File Analysis | Zeek File Analysis Framework | Analyze files observed in network traffic. |
| Hashing | MD5, SHA-1, SHA-256 analyzers | Generate file hashes for identification and correlation. |
| Package Management | ZKG | Manage Zeek packages and extensions. |
| Linux Utilities | wget, file, ip | Download test files, identify file types, and inspect network interfaces. |
| Log Formats | TSV, JSON | Represent and process structured network event records. |

## Learning Outcomes

- Deploy and manage Zeek using ZeekControl.
- Understand the purpose of Zeek network monitoring logs.
- Configure file hashing and identify files using cryptographic hashes.
- Generate structured JSON logs.
- Configure file extraction from monitored network traffic.
- Correlate connection, HTTP, notice, and file-related events.
- Use network telemetry to support malware investigations.

## Evidence Requirements

The original practical assignment consolidates the required evidence into a single PDF document.

[View Universal Class Evidence PDF](./evidences.pdf)

| Activity | Required Screenshot |
|---|---|
| 3.1 | Step 2 |
| 3.2 | Step 2 |
| 3.3 | Step 5 |
| 3.4 | Step 6 |
| 3.5 | Step 1 |

The universal evidence PDF consolidates the five screenshots required by the practical assignment.

## Technical Notes

- The reported lab results included a running Zeek service, SHA-256 hashing configuration, JSON log configuration, and extraction of a test PDF through the ens5 interface.
- The presence of a file record in files.log does not by itself prove that the file content was extracted to disk. Extraction requires an appropriate file extraction configuration.
- The suspicious executable and malware indicators described in Activity 3.5 belong to the training scenario. Example paths and sample metadata should not be assumed to represent independent malware validation.

## References

- [Zeek Documentation — Logs](https://docs.zeek.org/en/current/tutorial/logs.html)
- [Zeek Documentation — files.log](https://docs.zeek.org/en/current/reference/logs/files.html)
- [Zeek Documentation — File Analysis Framework](https://docs.zeek.org/en/current/frameworks/file-analysis.html)
- [ZeekControl — GitHub](https://github.com/zeek/zeekctl)
- [Zeek — Official Project](https://zeek.org/)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
