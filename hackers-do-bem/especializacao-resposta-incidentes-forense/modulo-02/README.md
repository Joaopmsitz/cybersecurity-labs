# Module 02 - Data Processing and Digital Investigation

This module covers practical activities involving security data collection, SIEM operations, threat intelligence, threat hunting, digital investigation, memory forensics, and disk and network evidence analysis.

## Activities — Class 06

| Activity | Topic | Description | View |
|---|---|---|---|
| 6.1 — Preparing Splunk to Receive Zeek Logs | SIEM Configuration | Inspect Zeek JSON logs and create a dedicated Splunk index. | [View](./aula-06/atividade-6.1-preparando-splunk-zeek/README.md) |
| 6.2 — Visualizing Zeek Logs in Splunk | Log Forwarding | Configure the Splunk Universal Forwarder and search for collected Zeek events. | [View](./aula-06/atividade-6.2-visualizando-logs-splunk/README.md) |
| 6.3 — Threat Hunting with Zeek | Threat Hunting | Investigate network connections, source and destination hosts, and traffic patterns using SPL. | [View](./aula-06/atividade-6.3-threat-hunting-zeek-splunk/README.md) |
| 6.4 — Preparing Elastic to Receive Zeek Logs | Elastic Stack | Start and validate Elasticsearch, Kibana, and Logstash services. | [View](./aula-06/atividade-6.4-preparando-elastic/README.md) |
| 6.5 — Sending Zeek Data to Elastic | Log Ingestion | Forward Zeek logs using Filebeat and investigate events in Kibana. | [View](./aula-06/atividade-6.5-enviando-zeek-elastic/README.md) |

## Activities — Class 07

| Activity | Topic | Description | View |
|---|---|---|---|
| 7.1 — Zeek Intelligence Framework | Threat Intelligence | Configure the Zeek Intelligence Framework and generate indicator match logs from PCAP traffic. | [View](./aula-07/atividade-7.1-zeek-intelligence-framework/README.md) |
| 7.2 — Analyzing Intelligence Matches | Indicator Analysis | Inspect `intel.log` and analyze positive matches between observed network data and intelligence indicators. | [View](./aula-07/atividade-7.2-analisando-correspondencias/README.md) |
| 7.3 — Using Threat Intelligence Sources | Threat Intelligence Feeds | Enrich Zeek with domain and IP indicators from external intelligence sources. | [View](./aula-07/atividade-7.3-fontes-inteligencia/README.md) |
| 7.4 — Threat Hunting with Zeek | Network Forensics | Process PCAP files and extract network metadata using Zeek and `zeek-cut`. | [View](./aula-07/atividade-7.4-threat-hunting-zeek/README.md) |
| 7.5 — Network Traffic Analysis with RITA | Beaconing Detection | Import Zeek logs into RITA and investigate suspicious beaconing and potential command-and-control communication. | [View](./aula-07/atividade-7.5-analise-trafego-rita/README.md) |

## Activities — Class 08

| Activity | Topic | Description | View |
|---|---|---|---|
| 8.1 — Network Investigation with p0f | Network Fingerprinting | Perform passive operating system fingerprinting and investigate observed IP addresses using WHOIS. | [View](./aula-08/atividade-8.1-investigacao-rede-p0f/README.md) |
| 8.2 — Post-Exploitation Assessment with Bashark | System Investigation | Examine the training environment and analyze a controlled loopback reverse-shell demonstration. | [View](./aula-08/atividade-8.2-pos-exploracao-bashark/README.md) |
| 8.3 — PDF Malware Analysis | Malware Analysis | Inspect PDF objects and identify suspicious embedded content using pdf-parser and PDFiD. | [View](./aula-08/atividade-8.3-analise-malware-pdf/README.md) |
| 8.4 — Malware Analysis with Hybrid Analysis | Sandbox Analysis | Submit the training PDF sample to a sandbox and examine its analysis report. | [View](./aula-08/atividade-8.4-hybrid-analysis/README.md) |
| 8.5 — Ransomware Memory Analysis with Volatility 3 | Memory Forensics | Examine a Windows memory image and identify operating system information using Volatility 3. | [View](./aula-08/atividade-8.5-analise-memoria-volatility/README.md) |

## Activities — Class 09

| Activity | Topic | Description | View |
|---|---|---|---|
| 9.1 — Preparing a Forensic Toolkit | Forensic Preparation | Prepare bootable Debian media and an external forensic workstation with disk analysis tools. | [View](./aula-09/atividade-9.1-preparacao-ferramenta-forense/README.md) |
| 9.2 — Collecting Physical Evidence | Forensic Acquisition | Perform bit-by-bit disk acquisition and verify image integrity using MD5 and SHA-256 hashes. | [View](./aula-09/atividade-9.2-coleta-evidencias-fisicas/README.md) |
| 9.3 — Analyzing the Disk and Filesystem | Filesystem Forensics | Examine disk metadata, filesystem characteristics, volume labels, sectors, and directory entries. | [View](./aula-09/atividade-9.3-analise-disco-filesystem/README.md) |
| 9.4 — Collecting Logical Evidence | File Recovery | Mount forensic images read-only, inspect file metadata, and recover embedded files using Foremost. | [View](./aula-09/atividade-9.4-coleta-evidencias-logicas/README.md) |
| 9.5 — Recovering Partitions and Data | Partition Recovery | Identify filesystem offsets in a damaged disk image and recover access to partition contents. | [View](./aula-09/atividade-9.5-recuperacao-particoes-dados/README.md) |

## Activities — Class 10

| Activity | Topic | Description | View |
|---|---|---|---|
| 10.1 — Linux Memory Dump with AVML | Memory Acquisition | Acquire volatile memory from a Linux system and generate cryptographic hashes of the resulting image. | [View](./aula-10/atividade-10.1-dump-memoria-linux/README.md) |
| 10.2 — Windows Memory Dump with FTK Imager | Memory Acquisition | Capture a Windows memory image using FTK Imager. | [View](./aula-10/atividade-10.2-dump-memoria-windows/README.md) |
| 10.3 — Logical Memory Evidence Collection | Memory Forensics | Analyze a Windows memory image using Volatility 3 plugins and preserve forensic results. | [View](./aula-10/atividade-10.3-evidencias-logicas-memoria/README.md) |
| 10.4 — Network Dump with tcpdump | Network Forensics | Capture network packets and generate integrity hashes for the resulting PCAP file. | [View](./aula-10/atividade-10.4-dump-rede-tcpdump/README.md) |
| 10.5 — Logical Network Evidence Collection with Wireshark | Network Forensics | Analyze packet captures, filter HTTP traffic, and export transferred objects using Wireshark. | [View](./aula-10/atividade-10.5-evidencias-logicas-rede-wireshark/README.md) |

## Evidence

Evidence files are organized by class. Each PDF consolidates the screenshots and supporting material required for the corresponding practical activities.

- [View Evidence — Class 06](./aula-06/evidences.pdf)
- [View Evidence — Class 07](./aula-07/evidences.pdf)
- [View Evidence — Class 08](./aula-08/evidences.pdf)
- [View Evidence — Class 09](./aula-09/evidences.pdf)
- [View Evidence — Class 10](./aula-10/evidences.pdf)

## Navigation

[Back to Specialization](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Cybersecurity Portfolio](../../../README.md)
