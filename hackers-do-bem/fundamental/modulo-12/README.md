# Module 12 — System Logs and Digital Forensics

This module covers practical activities involving Windows event logs, time synchronization, Linux logging, network traffic analysis, metadata examination, filesystem forensics, and disk image acquisition using Windows Server 2022 and Kali Linux.

## Activities — Classes 45–46

| Activity | Topic | Description | View |
|---|---|---|---|
| 12.01 — Exploring Logs in Windows Server 2022 | System Monitoring | Explore Windows event logs using Event Viewer and examine filtering options for application events. | [View](./aula-45-46/atividade-12.01-logs-windows-server-2022/README.md) |
| 12.02 — Enabling NTP on Windows Server 2022 | Time Synchronization | Configure Windows Time through Group Policy, specify an NTP server, restart the service, and inspect its status. | [View](./aula-45-46/atividade-12.02-ntp-windows-server-2022/README.md) |
| 12.03 — Exploring Logs on Kali Linux | Linux Logging | Explore `/var/log`, inspect `syslog` and the systemd journal, search for text using `grep`, and examine GNOME Logs. | [View](./aula-45-46/atividade-12.03-explorando-logs-kali/README.md) |
| 12.04 — Capturing Packets with Wireshark on Kali Linux | Network Traffic Analysis | Capture network traffic on `eth0`, filter HTTPS-related TCP traffic, and inspect a TCP stream to examine TLS encryption. | [View](./aula-45-46/atividade-12.04-capturando-pacotes-wireshark-kali/README.md) |
| 12.05 — Analyzing TLS Packets with tcpdump and Wireshark | Network Forensics | Capture HTTPS traffic using `tcpdump`, save packets in PCAP format, and analyze TLS traffic in Wireshark. | [View](./aula-45-46/atividade-12.05-analisando-pacotes-tls-tcpdump-wireshark/README.md) |

## Activities — Classes 47–48

| Activity | Topic | Description | View |
|---|---|---|---|
| 12.06 — Reading Metadata on Kali Linux | Metadata Forensics | Use ExifTool to examine metadata from JPEG images and PDF documents, including file properties, timestamps, and author information. | [View](./aula-47-48/atividade-12.06-ler-metadados-kali/README.md) |
| 12.07 — Removing Metadata on Kali Linux | Metadata Sanitization | Remove metadata from a JPEG image using ExifTool, inspect the resulting file, and compare it with the preserved original. | [View](./aula-47-48/atividade-12.07-apagando-metadados-kali/README.md) |
| 12.08 — Writing Metadata on Kali Linux | Metadata Manipulation | Add copyright and creator information to an image and modify its metadata date fields using ExifTool. | [View](./aula-47-48/atividade-12.08-escrevendo-metadados-kali/README.md) |
| 12.09 — Exploring The Sleuth Kit (TSK) on Kali Linux | Filesystem Forensics | Identify disk partitions, list filesystem entries with `fls`, and examine inode-related information using `ils`. | [View](./aula-47-48/atividade-12.09-explorando-tsk-kali/README.md) |
| 12.10 — Acquiring a Disk Image on Kali Linux | Digital Forensics | Create a block-level copy of a partition using `dd`, inspect the resulting file with `stat`, and remove the temporary image. | [View](./aula-47-48/atividade-12.10-aquisicao-imagem-disco-kali/README.md) |

## Evidence

Evidence files are organized by class group.

- [View Evidence — Classes 45–46](./aula-45-46/evidencias.pdf)
- [View Evidence — Classes 47–48](./aula-47-48/evidencias.pdf)

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Repository](../../../README.md)
