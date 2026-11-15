# Hackers do Bem - Specialization | Module 02 - Class 10

This class covers memory acquisition and analysis, network traffic capture, and logical evidence collection using forensic tools for Linux, Windows, and network environments.

The practical activities use AVML, FTK Imager, Volatility 3, tcpdump, and Wireshark.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 02 - Data Processing |
| Class | 10 |
| Main Topic | Memory and Network Dump Tools and Techniques |
| Main Technologies | AVML, FTK Imager, Volatility 3, tcpdump, Wireshark |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 10.1 | Linux Memory Dump | Acquire volatile memory from a Linux system using AVML and calculate cryptographic hashes. | [View Activity](./atividade-10.1-dump-memoria-linux/README.md) |
| 10.2 | Windows Memory Dump | Acquire a Windows memory image using FTK Imager. | [View Activity](./atividade-10.2-dump-memoria-windows/README.md) |
| 10.3 | Logical Memory Evidence Collection | Analyze a Windows memory image using Volatility 3 plugins and preserve extracted forensic results. | [View Activity](./atividade-10.3-evidencias-logicas-memoria/README.md) |
| 10.4 | Network Dump | Capture network packets using tcpdump and calculate capture integrity hashes. | [View Activity](./atividade-10.4-dump-rede-tcpdump/README.md) |
| 10.5 | Logical Network Evidence Collection | Analyze a network capture with Wireshark and export HTTP objects. | [View Activity](./atividade-10.5-evidencias-logicas-rede-wireshark/README.md) |

## Environment

The activities use the `forenseLinux` virtual machine and the `forensewin` Windows virtual machine provided by the training environment.

| Component | Purpose |
|---|---|
| AVML | Linux volatile memory acquisition |
| FTK Imager | Windows memory acquisition and forensic imaging |
| Volatility 3 | Memory image analysis |
| tcpdump | Network packet capture |
| Wireshark | Packet inspection and logical evidence extraction |
| Netcat | Not used in this class; network capture is performed with tcpdump |

## Tools and Technologies

- AVML
- FTK Imager
- Volatility 3
- tcpdump
- Wireshark
- MD5
- SHA-256
- PCAP
- Linux
- Windows
- Memory forensics
- Network forensics

## Learning Outcomes

- Acquire volatile memory from a Linux system.
- Generate and verify memory dump hashes.
- Understand Windows memory acquisition using FTK Imager.
- Identify operating system information from memory images.
- Extract forensic artifacts using Volatility 3.
- Capture network traffic using tcpdump.
- Preserve network captures and calculate integrity hashes.
- Analyze network packets with Wireshark.
- Filter HTTP traffic and export transferred objects.

## Evidence

A single PDF contains the screenshots required for four practical activities.

| Activity | Required Step | Evidence Description | PDF Page |
|---|---|---|---|
| 10.1 | Step 2 | Terminal showing the creation of `/home/aluno/forense`, the copy of AVML, and the prepared working directory. | 1 |
| 10.3 | Step 3 | Volatility 3 `windows.info` output displaying the memory image operating system metadata. | 2 |
| 10.4 | Step 2 | `ip a` output showing the active network interfaces and their assigned IP addresses. | 3 |
| 10.5 | Step 8 | Wireshark HTTP Export Objects view showing the objects identified in the network capture and the exported files. | 4 |

Activity 10.2 does not require a screenshot for this practical submission.

- [View consolidated evidence - evidences.pdf](./evidences.pdf)

## Technical Notes

- AVML is a Linux volatile memory acquisition tool. The training VM supplies a binary that uses the command syntax documented in the course; current upstream AVML uses the `acquire` subcommand.
- Memory acquisition may change system state. In real investigations, store the acquisition on a separate trusted external device whenever possible.
- Volatility 3 uses plugins and symbol tables to analyze memory images.
- The course's `windows.hashdump.Hashdump` plugin is documented as deprecated in current Volatility 3 documentation.
- Memory artifacts may contain credential hashes and other sensitive information. Do not publish raw memory dumps or credential extraction outputs.
- tcpdump supports packet filters and writing captures to PCAP files.
- Wireshark's Export Objects feature reconstructs objects transferred through supported protocols, including HTTP.
- Only capture traffic in networks and systems for which you have authorization.

## References

- [Microsoft - AVML](https://github.com/microsoft/avml)
- [Exterro - FTK Imager User Guide](https://d1kpmuwb7gvu1i.cloudfront.net/Imager/8.2/Exterro%20FTK%20Imager%208.2%20-%20User%20Guide-%20.pdf)
- [Volatility 3 - Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 - Windows Hashdump Plugin](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.windows.hashdump.html)
- [tcpdump - Manual](https://www.tcpdump.org/manpages/tcpdump.1.html)
- [Wireshark - Exporting Data](https://www.wireshark.org/docs/wsug_html_chunked/ChIOExportSection.html)
- [Wireshark - Display Filters](https://www.wireshark.org/docs/man-pages/wireshark-filter.html)

## Navigation

- [Module 02](../README.md)
- [Previous Class - 09](../aula-09/README.md)
- [Next Module - 03](../../modulo-03/README.md)
- [Specialization Overview](../../README.md)
