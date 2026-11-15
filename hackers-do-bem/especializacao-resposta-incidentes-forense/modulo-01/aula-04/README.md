# Lesson 04 — Incident Handling: Network and Web Application

**Training:** Hackers do Bem — Incident Response and Digital Forensics Specialization  
**Participant:** João Paulo Moreira de Sousa  
**Submission status:** Submitted for evaluation  
**Evaluation status:** Evaluated  
**Last modification recorded by the course platform:** May 11, 2026 — 21:01

## Overview

This lesson introduces Network Security Monitoring (NSM) and its relationship with Enterprise Security Monitoring (ESM). It explores how network traffic, endpoint telemetry, security logs, and incident response procedures can be combined to identify and investigate suspicious activity.

NSM is not limited to generating intrusion alerts. It also involves collecting and analyzing relevant network data so that an investigation can reconstruct events, identify attacker behavior, and support incident response.

The lesson discusses capabilities commonly found in an NSM environment, including:

- Network traffic monitoring and packet capture.
- Log collection, search, and visualization.
- Intrusion detection with tools such as Suricata and Snort.
- Threat hunting and investigation of suspicious activity.
- Incident case management and playbook execution.
- Endpoint and network telemetry correlation.

Security Onion is presented as an example of an open-source NSM platform integrating multiple security tools and investigation capabilities.

## Activities

| Activity | Subject | Evidence |
|---|---|---|
| 4.1 | CyberChef — XOR brute-force decoding | [Page 1](./evidences.pdf) |
| 4.2 | CyberChef — Morse code decoding | [Page 2](./evidences.pdf) |
| 4.3 | Malware incident response playbook | [Pages 5–7](./evidences.pdf) |
| 4.4 | Sigma rule conversion to ElastAlert | [Page 3](./evidences.pdf) |
| 4.5 | MITRE ATT&CK Navigator — APT3 and APT29 | [Page 4](./evidences.pdf) |

## Repository structure

    aula-04/
    ├── README.md
    ├── evidences.pdf
    ├── atividade-4.1-cyberchef-xor-brute-force/
    │   └── README.md
    ├── atividade-4.2-cyberchef-morse-decoding/
    │   └── README.md
    ├── atividade-4.3-malware-incident-response-playbook/
    │   └── README.md
    ├── atividade-4.4-sigma-to-elastalert/
    │   └── README.md
    └── atividade-4.5-mitre-attack-navigator-apt3-apt29/
        └── README.md

## Evidence file

All activity screenshots and the written playbook deliverable are consolidated into a single PDF:

[View Universal Class Evidence PDF](./evidences.pdf)

The PDF contains the evidence pages in the following order:

1. Activity 4.1 — XOR Brute Force result.
2. Activity 4.2 — final Morse decoding result.
3. Activity 4.4 — Sigma-to-ElastAlert conversion.
4. Activity 4.5 — combined APT3 and APT29 layer.
5. Activity 4.3 — incident response playbook, pages 5–7.

Each activity README describes its objective, procedure, configuration, result, and technical relevance.
