# Hackers do Bem - Specialization | Module 02 - Class 08

This class covers digital investigation techniques involving network fingerprinting, post-exploitation assessment in a controlled lab, PDF malware analysis, automated sandbox analysis, and memory forensics.

The practical activities use p0f, Bashark, PDFiD, pdf-parser, Hybrid Analysis, and Volatility 3.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 02 - Data Processing |
| Class | 08 |
| Main Topic | Investigation Process |
| Main Technologies | p0f, Bashark, PDFiD, pdf-parser, Hybrid Analysis, Volatility 3 |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 8.1 | Network Investigation with p0f | Passively identify remote operating systems and investigate observed IP addresses using WHOIS. | [View Activity](./atividade-8.1-investigacao-rede-p0f/README.md) |
| 8.2 | Post-Exploitation Assessment with Bashark | Explore system information and a loopback reverse-shell demonstration in the isolated lab. | [View Activity](./atividade-8.2-pos-exploracao-bashark/README.md) |
| 8.3 | PDF Malware Analysis | Inspect PDF objects and identify suspicious embedded elements using pdf-parser and PDFiD. | [View Activity](./atividade-8.3-analise-malware-pdf/README.md) |
| 8.4 | Malware Analysis with Hybrid Analysis | Submit the lab PDF sample for sandbox analysis and examine its public report. | [View Activity](./atividade-8.4-hybrid-analysis/README.md) |
| 8.5 | Ransomware Memory Analysis with Volatility 3 | Inspect a Windows memory image and identify operating system information. | [View Activity](./atividade-8.5-analise-memoria-volatility/README.md) |

## Environment

The practical activities use the `forenseLinux` virtual machine provided by the training environment.

| Component | Purpose |
|---|---|
| p0f | Passive operating system fingerprinting |
| Bashark | Linux post-exploitation assessment in the training environment |
| Netcat | Local network connection listener |
| pdf-parser | PDF object and embedded content inspection |
| PDFiD | PDF structural keyword analysis |
| Hybrid Analysis | Automated malware sandbox analysis |
| Volatility 3 | Memory forensics |
| WHOIS | IP registration and network ownership lookup |

## Tools and Technologies

- p0f
- Bashark
- Netcat / Ncat
- WHOIS
- PDFiD
- pdf-parser
- Hybrid Analysis
- Volatility 3
- Python 3
- Linux
- Memory forensics
- Network forensics
- Malware analysis

## Learning Outcomes

- Perform passive network operating system fingerprinting.
- Investigate observed IP addresses using WHOIS.
- Examine system information in an authorized lab environment.
- Understand local reverse-shell demonstrations and their network behavior.
- Inspect PDF objects and embedded content.
- Identify suspicious PDF structural keywords.
- Interpret automated sandbox analysis reports.
- Identify operating system information from memory images.
- Apply forensic analysis techniques to suspicious files and memory artifacts.

## Evidence

A single PDF contains the screenshots required for all five practical activities.

| Activity | Required Step | Evidence Description | PDF Page |
|---|---|---|---|
| 8.1 | Step 8 | Side-by-side terminals showing p0f network activity and the WHOIS lookup of an observed IP address. | 1 |
| 8.2 | Step 8 | Terminal showing the successful loopback Netcat connection and the `pwd` and `ls` command outputs. | 2 |
| 8.3 | Step 5 | PDFiD output displaying structural keyword counts, including JavaScript-related indicators. | 3 |
| 8.4 | Step 2 | Hybrid Analysis public report showing the selected sandbox environment and the analysis results for `testpdf.pdf`. | 4 |
| 8.5 | Step 2 | Volatility 3 `windows.info` output identifying the operating system in `wcry.raw`. | 5 |

- [View consolidated evidence - evidences.pdf](./evidences.pdf)

The PDF is stored at the class level and consolidates the five required screenshots.

## Technical Notes

- p0f performs passive fingerprinting by observing network traffic rather than actively scanning remote hosts.
- Operating system fingerprint results depend on the traffic observed and the available fingerprint database.
- Bashark and reverse-shell demonstrations must remain restricted to the authorized and isolated training environment. The documented listener and connection use loopback address `127.0.0.1`.
- PDFiD keyword counts are triage indicators, not proof that a PDF is malicious.
- Hybrid Analysis submissions configured as public reports should not contain confidential, proprietary, or personal documents.
- Volatility 3 uses plugins to extract information from memory images. The `windows.info` plugin provides operating system information.
- The course-provided paths and sample files refer to the supplied training VM.

## References

- [Kali Linux - p0f](https://www.kali.org/tools/p0f/)
- [Ncat - Network Communication Tool](https://nmap.org/ncat/)
- [Didier Stevens - PDF Tools](https://blog.didierstevens.com/programs/pdf-tools/)
- [Hybrid Analysis](https://www.hybrid-analysis.com/)
- [CrowdStrike - Sandbox Scryer](https://www.crowdstrike.com/en-us/blog/sandbox-scryer-free-threat-hunting-tool/)
- [Volatility 3 - Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 - Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
## Navigation

- [Module 02](../README.md)
- [Previous Class - 07](../aula-07/README.md)
- [Next Class - 09](../aula-09/README.md)
- [Specialization Overview](../../README.md)
