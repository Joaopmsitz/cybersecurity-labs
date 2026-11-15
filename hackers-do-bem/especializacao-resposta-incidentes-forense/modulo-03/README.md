# Hackers do Bem — Specialization | Module 03 — Computer Forensics

Documentation of the third module of the Hackers do Bem Incident Response and Digital Forensics specialization.

This module covers practical activities involving computer forensics, filesystem examination, timeline reconstruction, memory analysis, network forensics, and web attack investigation.

## Module Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 03 — Computer Forensics |
| Classes | 05 |
| Practical Activities | 25 |
| Main Topics | Disk forensics, Windows and Linux artifacts, memory forensics, network evidence, web attacks, and incident investigation |

## Activities — Class 01 (Aula 11)

**Computer Forensics — Timeline, Investigation, Password Auditing, and Steganography**

| Activity | Topic | Description | View |
|---|---|---|---|
| 11.1 — Timeline Analysis with mactime | Timeline Reconstruction | Generate and examine a forensic timeline using filesystem bodyfile metadata and mactime. | [View](./aula-11/atividade-11.1-linha-do-tempo-mactime/README.md) |
| 11.2 — Evidence Reconstruction with Autopsy | Disk Forensics | Examine recovered files and reconstruct relevant facts from forensic disk evidence. | [View](./aula-11/atividade-11.2-reconstrucao-fatos-autopsy/README.md) |
| 11.3 — Password Auditing with John the Ripper | Password Analysis | Analyze password hashes and perform controlled password recovery using John the Ripper. | [View](./aula-11/atividade-11.3-john-the-ripper/README.md) |
| 11.4 — ZIP Password Recovery with fcrackzip | Archive Forensics | Examine a protected ZIP archive and evaluate password recovery using fcrackzip. | [View](./aula-11/atividade-11.4-senha-arquivo-zip-fcrackzip/README.md) |
| 11.5 — Image Steganography with Steghide | Steganography | Investigate an image file and extract embedded data using Steghide. | [View](./aula-11/atividade-11.5-esteganografia-steghide/README.md) |

## Activities — Class 02 (Aula 12)

**Windows and Linux Artifact Analysis**

| Activity | Topic | Description | View |
|---|---|---|---|
| 12.1 — Browser History Analysis | Browser Forensics | Examine browser history records in SQLite and convert browser timestamps into readable dates. | [View](./aula-12/atividade-12.1-historico-navegacao/README.md) |
| 12.2 — User Directories and Recycle Bin | Windows Filesystem Forensics | Examine Windows user directories, hidden files, user-specific Recycle Bin structures, and deleted-file artifacts. | [View](./aula-12/atividade-12.2-diretorios-usuario/README.md) |
| 12.3 — Linux Configuration File Analysis | Configuration Forensics | Inspect Linux configuration artifacts, shell startup files, FTP-related files, and suspicious account entries. | [View](./aula-12/atividade-12.3-arquivos-configuracao/README.md) |
| 12.4 — Linux Log Analysis | Log Forensics | Examine authentication logs, system activity, and shell history to reconstruct suspicious account activity. | [View](./aula-12/atividade-12.4-logs-linux/README.md) |
| 12.5 — NTFS Alternate Data Streams | Filesystem Forensics | Identify and examine NTFS Alternate Data Streams (ADS) using Windows tools. | [View](./aula-12/atividade-12.5-alternate-data-streams/README.md) |

## Activities — Class 03 (Aula 13)

**Memory Forensics — Linux Core Dumps, Windows Minidumps, and Volatility**

| Activity | Topic | Description | View |
|---|---|---|---|
| 13.1 — Linux Core File Analysis | Memory Forensics | Generate a controlled application crash and examine the resulting Linux core dump using strings. | [View](./aula-13/atividade-13.1-core-files-linux/README.md) |
| 13.2 — Windows Minidump Analysis with WinDbg | Crash Dump Analysis | Examine a Windows minidump and investigate crash information using the WinDbg `!analyze -v` command. | [View](./aula-13/atividade-13.2-minidump-windows/README.md) |
| 13.3 — User Evidence in Memory | Memory Forensics | Examine a Windows memory image with Volatility to identify user-related environment variables and file artifacts. | [View](./aula-13/atividade-13.3-evidencias-usuarios-memoria/README.md) |
| 13.4 — Active Process Analysis | Process Forensics | Examine process listings, parent-child relationships, and command-line artifacts using Volatility. | [View](./aula-13/atividade-13.4-analise-processos-ativos/README.md) |
| 13.5 — Network Artifacts in Memory | Network Forensics | Investigate memory-resident network artifacts and evaluate plugin compatibility with the target Windows version. | [View](./aula-13/atividade-13.5-artefatos-rede-memoria/README.md) |

## Activities — Class 04 (Aula 14)

**Network Forensics — TCPFlow, Foremost, NetworkMiner, and Wireshark**

| Activity | Topic | Description | View |
|---|---|---|---|
| 14.1 — Network Evidence Extraction with TCPFlow and Foremost | Network Forensics | Reconstruct TCP streams and recover image files from network-related data using file carving. | [View](./aula-14/atividade-14.1-tcpflow-foremost/README.md) |
| 14.2 — Image Evidence Analysis with NetworkMiner | Network Forensics | Examine a PCAP and inspect image artifacts automatically reconstructed by NetworkMiner. | [View](./aula-14/atividade-14.2-networkminer-imagens/README.md) |
| 14.3 — SMTP Email and Credential Analysis | Protocol Forensics | Examine SMTP authentication artifacts and identify credential exposure in captured network traffic. | [View](./aula-14/atividade-14.3-networkminer-smtp/README.md) |
| 14.4 — Wireless Network Analysis with Wireshark | Wireless Forensics | Configure IEEE 802.11 decryption settings and examine WPA-protected wireless traffic. | [View](./aula-14/atividade-14.4-wireshark-wifi/README.md) |
| 14.5 — Nmap Scan Analysis with Wireshark | Network Attack Analysis | Filter TCP traffic and investigate packet patterns associated with sequential port scanning. | [View](./aula-14/atividade-14.5-wireshark-nmap/README.md) |

## Activities — Class 05 (Aula 15)

**Web Attack Investigation — SQL Injection, XSS, File Upload, and Brute Force**

| Activity | Topic | Description | View |
|---|---|---|---|
| 15.1 — Investigating SQL Injection Attacks | Web Application Forensics | Examine SQL Injection activity in DVWA and identify attack requests in Apache access logs. | [View](./aula-15/atividade-15.1-sql-injection/README.md) |
| 15.2 — Investigating Reflected XSS | Web Application Forensics | Investigate reflected JavaScript injection and correlate browser activity with HTTP access logs. | [View](./aula-15/atividade-15.2-xss-refletido/README.md) |
| 15.3 — Investigating Stored XSS | Web Application Forensics | Examine persistent script content in the DVWA database and correlate stored artifacts with application activity. | [View](./aula-15/atividade-15.3-xss-persistente/README.md) |
| 15.4 — Investigating File Upload Attacks | Web Server Forensics | Examine uploaded PHP artifacts, server-side file metadata, and evidence associated with unauthorized execution. | [View](./aula-15/atividade-15.4-file-upload/README.md) |
| 15.5 — Investigating Brute-Force Attacks | Authentication Forensics | Analyze automated login attempts and identify Hydra-related indicators in Apache access logs. | [View](./aula-15/atividade-15.5-forca-bruta/README.md) |

## Evidence

Evidence files are organized by class. Each PDF consolidates the screenshots and supporting material required for the corresponding practical activities.

| Class | Evidence | Description |
|---|---|---|
| Class 01 — Aula 11 | [View Evidence — Class 01](./aula-11/evidences.pdf) | Timeline analysis, Autopsy investigation, password auditing, ZIP recovery, and steganography. |
| Class 02 — Aula 12 | [View Evidence — Class 02](./aula-12/evidences.pdf) | Browser history, Windows user directories, configuration files, Linux logs, and NTFS ADS. |
| Class 03 — Aula 13 | [View Evidence — Class 03](./aula-13/evidences.pdf) | Linux core files, Windows minidumps, memory user artifacts, process analysis, and network artifacts. |
| Class 04 — Aula 14 | [View Evidence — Class 04](./aula-14/evidences.pdf) | TCPFlow, Foremost, NetworkMiner, SMTP analysis, wireless decryption, and Nmap traffic analysis. |
| Class 05 — Aula 15 | [View Evidence — Class 05](./aula-15/evidences.pdf) | SQL Injection, reflected and stored XSS, file upload, and brute-force investigation. |

## Documentation Structure

Each class contains individual technical activity directories.

Each activity README documents:

- Objective and environment.
- Technical concepts and tools.
- Procedures and commands.
- Relevant outputs and findings.
- Technical analysis and interpretation.
- Concepts practiced.
- Evidence and references.

The class evidence PDFs are stored separately at the corresponding class directory level.

## Navigation

- [Specialization Overview](../README.md)
- [Previous Module — 02: Data Processing and Digital Investigation](../modulo-02/README.md)
- [Hackers do Bem](../../README.md)
- [Cybersecurity Labs](../../../README.md)
