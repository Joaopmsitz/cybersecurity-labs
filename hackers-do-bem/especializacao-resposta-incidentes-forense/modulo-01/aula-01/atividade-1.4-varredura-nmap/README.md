# Activity 1.4 — DNS Reconnaissance and Nmap Scanning

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Documented

## Objective

Explore DNS information gathering, reverse DNS resolution, and network scanning with Nmap.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| DNS Tools | nslookup, dig |
| Network Scanner | Nmap |
| Target | scanme.nmap.org |
| Target IPv4 | 45.33.32.156 |

## Procedure

### 1. Resolve a Hostname

Use `nslookup` to obtain DNS information:

```bash
nslookup scanme.nmap.org
```

The exercise material provides the following IPv4 address as an example:

```text
45.33.32.156
```

If nslookup is unavailable, use:

```bash
dig scanme.nmap.org
```

### 2. Perform a Reverse DNS Lookup

Query the IP address:

```bash
nslookup 45.33.32.156
```

The reverse lookup can return the associated hostname through a PTR record.

### 3. Scan the Target with Nmap

Execute:

```bash
nmap scanme.nmap.org -vv
```

The `-vv` option enables more detailed output during the scan.

The results provide information about discovered ports and their states.

## Technical Analysis

DNS resolution helps identify the IP address associated with a hostname.

Reverse DNS lookup performs the complementary operation by querying the DNS infrastructure for a name associated with an IP address.

Nmap extends this reconnaissance process by identifying network services exposed through accessible ports.

## Result

The activity demonstrates forward and reverse DNS lookup and introduces detailed network scanning with Nmap.

## Concepts Practiced

- DNS resolution
- Reverse DNS and PTR records
- Network reconnaissance
- Port discovery
- Nmap command-line options
- Interpretation of scan results

## Authorization and Responsible Use

The original training material identifies scanme.nmap.org as a controlled target for learning and limited scanning.

Scanning other systems requires appropriate authorization.

## Evidence

The assignment requests a screenshot of Step 3, showing the Nmap command and its output.

[Class Evidence PDF](../evidencias.pdf)

---

[Back to Class 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
