# Activity 1.3 — Web Reconnaissance with FinalRecon

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Documented

## Objective

Explore FinalRecon, an open-source reconnaissance tool designed to collect information about web targets.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | FinalRecon |
| Language | Python 3 |
| Installation Path | /opt/FinalRecon |

## Tool Overview

FinalRecon provides modular reconnaissance capabilities, including:

- WHOIS information
- HTTP header inspection
- SSL certificate information
- DNS enumeration
- Subdomain discovery
- Traceroute information
- Directory discovery
- Port scanning
- Web crawling

## Procedure

### 1. Display Help

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py -h
```

This displays the available options and usage information.

### 2. Inspect SSL Information

Run the SSL information module against a known website:

```bash
python3 /opt/FinalRecon/finalrecon.py --sslinfo --url https://www.google.com
```

The command retrieves information related to the target's SSL certificate.

### 3. Explore Additional Modules

HTTP headers:

```bash
python3 /opt/FinalRecon/finalrecon.py --headers --url https://www.google.com
```

WHOIS information:

```bash
python3 /opt/FinalRecon/finalrecon.py --whois --url https://www.google.com
```

Web crawling:

```bash
python3 /opt/FinalRecon/finalrecon.py --crawl --url https://www.google.com
```

Full reconnaissance:

```bash
python3 /opt/FinalRecon/finalrecon.py --full --url https://www.google.com
```

## Result

The activity explores FinalRecon's modular reconnaissance features and demonstrates how to request different types of information about a web target.

## Concepts Practiced

- Web reconnaissance
- SSL certificate inspection
- HTTP header analysis
- WHOIS information gathering
- Web crawling
- Automated reconnaissance tools

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
