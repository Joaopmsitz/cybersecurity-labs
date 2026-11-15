# Hackers do Bem — Specialization | Module 01 — Class 01

This class introduces cyber threats and the reconnaissance techniques used during the initial phases of security assessments. The practical activities explore network programming, TCP port scanning, web reconnaissance, DNS investigation, and information gathering.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 01 |
| Activities | 5 |
| Main Topics | Cyber Threats, Cyber Kill Chain, Network Reconnaissance, Port Scanning, DNS Investigation, and Information Gathering |

## Practical Activities

| Activity | Topic | Description | Documentation |
| -------- | ----- | ----------- | ------------- |
| 1.1 — Information Gathering with Python Sockets | Network Programming | Develop and analyze a basic client-server application using Python TCP sockets. | [View Activity](./atividade-1.1-coleta-informacoes/README.md) |
| 1.2 — TCP Port Scanner using Python Sockets | Port Scanning | Build a Python TCP scanner to identify open ports within a specified target port range. | [View Activity](./atividade-1.2-port-scanner-socket/README.md) |
| 1.3 — Web Reconnaissance with FinalRecon | Web Reconnaissance | Inspect SSL information, HTTP headers, WHOIS data, and web resources using FinalRecon. | [View Activity](./atividade-1.3-reconhecimento-finalrecon/README.md) |
| 1.4 — DNS Reconnaissance and Nmap Scanning | Network Discovery | Perform forward and reverse DNS lookups and investigate network ports using Nmap. | [View Activity](./atividade-1.4-varredura-nmap/README.md) |
| 1.5 — Information Gathering with cURL and DMitry | Information Gathering | Collect IP intelligence and domain information using cURL, IPinfo, and DMitry. | [View Activity](./atividade-1.5-outras-ferramentas-curl-dmitry/README.md) |

## Environment

All activities were performed in the `forenseLinux` virtual machine, accessed through the landing system using Remote Desktop Protocol (RDP).

| Component | Details |
|---|---|
| Virtual Machine | forenseLinux |
| Access Host | 192.168.98.10 |
| Programming Language | Python 3 |
| Network Tools | Nmap, nslookup, dig |
| Reconnaissance Tools | FinalRecon, DMitry |
| Information Service | IPinfo |

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Network Programming | Python 3, Socket | Implement TCP client-server communication. |
| Port Scanning | Python Socket, Nmap | Identify accessible hosts and listening ports. |
| Web Reconnaissance | FinalRecon | Inspect SSL certificates, HTTP headers, WHOIS information, and web resources. |
| DNS Investigation | nslookup, dig | Perform forward and reverse name resolution. |
| IP Intelligence | cURL, IPinfo | Retrieve IP registration and network-related information. |
| Domain Reconnaissance | DMitry | Collect WHOIS, subdomain, email, and port information. |

## Learning Outcomes

- Understand TCP socket communication and client-server architecture.
- Distinguish TCP stream sockets from UDP datagram sockets.
- Develop a basic TCP port scanner using Python.
- Perform web reconnaissance and inspect SSL information.
- Investigate forward and reverse DNS records.
- Interpret Nmap port scanning results.
- Collect IP and domain intelligence using reconnaissance tools.

## Evidence Requirements

The original practical assignment consolidates the required evidence into a single PDF document.

[View Universal Class Evidence PDF](./evidences.pdf)

| Activity | Required Screenshot |
|---|---|
| 1.1 | Step 7 |
| 1.2 | Step 3 |
| 1.3 | Step 2 |
| 1.4 | Step 3 |
| 1.5 | Step 3 |

The universal evidence PDF consolidates the five screenshots required by the practical assignment.

## Technical Notes

- The first activity is described in the course material as a UDP Echo Server, but the supplied implementation uses TCP stream sockets (SOCK_STREAM) and sends a fixed confirmation message rather than echoing the received payload.
- The Python port scanner uses range(70, 81), which tests ports 70 through 80, inclusive.
- Expected scan results from the training material should be distinguished from independently verified execution results.

## References

- [Python Socket Documentation](https://docs.python.org/3/library/socket.html)
- [Python Socket Programming HOWTO](https://docs.python.org/3/howto/sockets.html)
- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [FinalRecon — GitHub](https://github.com/thewhiteh4t/FinalRecon)
- [Kali Linux — DMitry](https://www.kali.org/tools/dmitry/)
- [IPinfo Developer Documentation](https://ipinfo.io/developers)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
