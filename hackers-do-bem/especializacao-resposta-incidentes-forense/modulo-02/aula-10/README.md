# Class 10 — Memory Forensics and Network Evidence Collection

This class covers the acquisition and examination of volatile memory from Linux and Windows systems, followed by network packet collection and HTTP object extraction.

The practical activities introduce AVML, FTK Imager, Volatility 3, tcpdump, and Wireshark as part of a digital forensic workflow.

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 10.1 — Linux Memory Dump with AVML | Linux Memory Acquisition | Acquire volatile memory from the forenseLinux virtual machine and generate MD5 and SHA-256 hashes for integrity verification. | [View](.//README.md) |
| 10.2 — Windows Memory Dump with FTK Imager | Windows Memory Acquisition | Capture volatile memory from a live Windows workstation using FTK Imager. | [View](.//README.md) |
| 10.3 — Windows Memory Analysis with Volatility 3 | Memory Forensics | Examine Windows kernel information and account hash artifacts from the acquired memory image. | [View](.//README.md) |
| 10.4 — Network Dump with tcpdump | Network Forensics | Inspect Linux network interfaces and capture packets into a PCAP file using tcpdump. | [View](.//README.md) |
| 10.5 — Logical Network Evidence Collection with Wireshark | Network Forensics | Analyze the packet capture and export reconstructed HTTP objects using Wireshark. | [View](.//README.md) |

## Environment and Tools

| Component | Description |
|---|---|
| Linux Environment | forenseLinux |
| Windows Environment | Windows forensic workstation |
| Linux Memory Acquisition | AVML |
| Windows Memory Acquisition | FTK Imager |
| Memory Analysis | Volatility 3 |
| Network Interface Inspection | ip a |
| Network Capture | tcpdump |
| Packet Analysis | Wireshark |
| Evidence Format | Memory images and PCAP files |
| Integrity Verification | MD5 and SHA-256 |

## Learning Outcomes

- Acquire volatile memory from Linux and Windows systems.
- Prepare memory images for forensic examination.
- Generate cryptographic hashes to support evidence integrity verification.
- Identify operating system information from Windows memory.
- Examine account-related artifacts using Volatility 3.
- Inspect Linux network interfaces.
- Capture packets using tcpdump.
- Analyze PCAP files in Wireshark.
- Export reconstructed HTTP objects from network traffic.
- Preserve and correlate forensic artifacts from different sources.

## Evidence

The consolidated PDF contains the screenshots required by the practical activities in this class.

[View Evidence — Class 10](./evidences.pdf)

## Technical Notes

- AVML is used for Linux volatile memory acquisition.
- FTK Imager is used to acquire memory from the live Windows workstation.
- Volatility 3 analyzes acquired memory images; it does not perform the acquisition in this workflow.
- The legacy windows.hashdump implementation is deprecated in current Volatility 3 documentation. The current replacement is windows.registry.hashdump.
- tcpdump uses -w to save captured packet data to a file for later analysis.
- Wireshark's Export Objects function can reconstruct HTTP objects from available protocol streams.
- Actual memory sizes, hashes, network interface addresses, packet counts, and exported object metadata are environment-specific and should be taken from the original evidence rather than estimated.

## Navigation

[Back to Module 02](../README.md) · [Back to Specialization](../../README.md) · [Back to Hackers do Bem](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
