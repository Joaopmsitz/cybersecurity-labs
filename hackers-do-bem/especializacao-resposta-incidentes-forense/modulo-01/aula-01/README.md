# Hackers do Bem — Specialization | Module 01 — Class 01

Documentation of the practical activities from Class 01 of the Hackers do Bem Incident Response and Digital Forensics specialization.

The class introduces cyber threats, information gathering, network reconnaissance, port scanning, DNS investigation, and technical tools used during the initial phases of security assessments.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 01 |
| Activities | 5 |
| Environment | forenseLinux VM |
| VM Address | 192.168.98.10 |
| Main Topics | Cyber Threats and Kill Chain Methodology |

## Practical Activities

| Activity | Topic | Documentation |
|---|---|---|
| 1.1 | Information Gathering with Python Sockets | [View Activity](./atividade-1.1-coleta-informacoes/) |
| 1.2 | TCP Port Scanner using Python Sockets | [View Activity](./atividade-1.2-port-scanner-socket/) |
| 1.3 | Web Reconnaissance with FinalRecon | [View Activity](./atividade-1.3-reconhecimento-finalrecon/) |
| 1.4 | DNS Reconnaissance and Nmap Scanning | [View Activity](./atividade-1.4-varredura-nmap/) |
| 1.5 | Information Gathering with cURL and DMitry | [View Activity](./atividade-1.5-outras-ferramentas-curl-dmitry/) |

## Environment

All activities were performed in the forenseLinux virtual machine, accessed through the landing system using Remote Desktop Protocol (RDP).

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
| Network Programming | Python, Socket | TCP client-server communication |
| Port Scanning | Python Socket, Nmap | Discover listening ports |
| Web Reconnaissance | FinalRecon | SSL, WHOIS, HTTP headers, and crawling |
| DNS Investigation | nslookup, dig | Forward and reverse name resolution |
| IP Intelligence | cURL, IPinfo | Retrieve IP registration and geolocation data |
| Domain Reconnaissance | DMitry | WHOIS, subdomains, email addresses, and port scanning |

## Learning Outcomes

- Understand network socket communication.
- Distinguish TCP stream sockets from UDP datagram sockets.
- Create a basic client-server application.
- Develop a TCP port scanner using Python.
- Perform web reconnaissance.
- Inspect SSL certificates and HTTP headers.
- Perform forward and reverse DNS resolution.
- Interpret Nmap port scanning results.
- Retrieve IP information through HTTP requests.
- Collect domain information with DMitry.
- Document reconnaissance results and technical findings.

## Evidence Requirements

The original assignment requires one PDF containing the five specified screenshots.

| Activity | Required Screenshot |
|---|---|
| 1.1 | Step 7 |
| 1.2 | Step 3 |
| 1.3 | Step 2 |
| 1.4 | Step 3 |
| 1.5 | Step 3 |

[View Universal Class Evidence PDF](./evidences.pdf)

The same evidence document is referenced by all five activity READMEs.

## Technical Notes

The original training material describes the first socket activity as a UDP Echo Server, but the supplied implementation uses TCP stream sockets and sends a fixed confirmation message.

The Python port scanner uses `range(70, 81)`, which tests ports 70 through 80, inclusive.

Expected scan results from the training material are identified separately from independently verified execution results.

## References

- [Python Socket Documentation](https://docs.python.org/3/library/socket.html)
- [Python Socket Programming HOWTO](https://docs.python.org/3/howto/sockets.html)
- [Nmap Documentation](https://nmap.org/book/)
- [Nmap Scanme Legal Information](https://nmap.org/book/legal-issues.html)
- [FinalRecon](https://github.com/thewhiteh4t/FinalRecon)
- [Kali Linux — DMitry](https://www.kali.org/tools/dmitry/)
- [IPinfo](https://ipinfo.io/)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
