# Hackers do Bem — Fundamental | Module 12

This module covers practical activities involving Windows event logs, time synchronization, Linux logging, network traffic analysis, metadata examination, filesystem forensics, and disk image acquisition using Windows Server 2022 and Kali Linux.

## Activities

### Activities — Class 45–46

| Activity | Topic | Description | View |
|---|---|---|---|
| 12.01 — Exploring Logs in Windows Server 2022 | Cybersecurity Practice | Explore the main event logs available in Windows Server 2022 through Event Viewer (eventvwr.msc), identify different log categories, and use event filtering to narrow down the displayed records. | [View](./aula-45-46/atividade-12.01-logs-windows-server-2022/README.md) |
| 12.02 — Enabling NTP on Windows Server 2022 | Cybersecurity Practice | Configure the Windows Time (W32Time) service on Windows Server 2022 to use NTP (Network Time Protocol), enabling the NTP server and client through Group Policy and configuring the server time.google.com. | [View](./aula-45-46/atividade-12.02-ntp-windows-server-2022/README.md) |
| 12.03 — Exploring Logs on Kali Linux | Cybersecurity Practice | Explore the main event logging files and tools available on Kali Linux, using the /var/log directory, the syslog file, journalctl, and the GNOME Logs graphical application. | [View](./aula-45-46/atividade-12.03-explorando-logs-kali/README.md) |
| 12.04 — Capturing Packets with Wireshark on Kali Linux | Cybersecurity Practice | Capture network traffic on Kali Linux using Wireshark, access an HTTPS website while the capture is running, and analyze the transmitted packets. | [View](./aula-45-46/atividade-12.04-capturando-pacotes-wireshark-kali/README.md) |
| 12.05 — Analyzing TLS Packets with tcpdump and Wireshark | Cybersecurity Practice | Capture and analyze HTTPS traffic using tcpdump and Wireshark, identify a TLS connection, and verify the protocol version used in the communication. | [View](./aula-45-46/atividade-12.05-analisando-pacotes-tls-tcpdump-wireshark/README.md) |

### Activities — Class 47–48

| Activity | Topic | Description | View |
|---|---|---|---|
| 12.06 — Reading Metadata on Kali Linux | Cybersecurity Practice | - Identify metadata present in digital files. - Use ExifTool to analyze files. - Examine information from JPEG and PDF files. - Understand how metadata can provide relevant information during forensic analysis. | [View](./aula-47-48/atividade-12.06-ler-metadados-kali/README.md) |
| 12.07 — Removing Metadata on Kali Linux | Cybersecurity Practice | - Remove metadata from an image. - Identify the differences between the original file and the processed file. - Use ExifTool for metadata sanitization. - Observe which information remains after removal. | [View](./aula-47-48/atividade-12.07-apagando-metadados-kali/README.md) |
| 12.08 — Writing Metadata on Kali Linux | Cybersecurity Practice | - Write metadata to digital files. - Modify copyright and authorship information. - Change dates stored in metadata. - Examine the results of these changes using ExifTool. | [View](./aula-47-48/atividade-12.08-escrevendo-metadados-kali/README.md) |
| 12.09 — Exploring The Sleuth Kit (TSK) on Kali Linux | Cybersecurity Practice | - Identify available disk partitions. - Use The Sleuth Kit tools. - List files and directories within a partition. - Query information related to inodes and their timestamps. | [View](./aula-47-48/atividade-12.09-explorando-tsk-kali/README.md) |
| 12.10 — Acquiring a Disk Image on Kali Linux | Cybersecurity Practice | - Identify available disk partitions. - Use dd to perform a block-level copy. - Create a partition image in a file. - Verify the size and attributes of the acquired file. | [View](./aula-47-48/atividade-12.10-aquisicao-imagem-disco-kali/README.md) |

## Evidence

Evidence files are organized by class. Each PDF consolidates the screenshots and supporting material required for the corresponding practical activities.

- [View Evidence — Class 45–46](./aula-45-46/evidencias.pdf)
- [View Evidence — Class 47–48](./aula-47-48/evidencias.pdf)

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Cybersecurity Portfolio](../../../README.md)
