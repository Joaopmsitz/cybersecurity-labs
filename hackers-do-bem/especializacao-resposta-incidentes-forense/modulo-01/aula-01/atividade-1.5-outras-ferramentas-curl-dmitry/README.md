# Activity 1.5 — Information Gathering with cURL and DMitry

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Documented

## Objective

Explore additional information-gathering tools, using cURL with IPinfo and DMitry for domain reconnaissance.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tools | cURL, DMitry |
| IP Intelligence Service | IPinfo |
| Example IP | 45.33.32.156 |
| Example Domain | google.com |

## Procedure

### 1. Retrieve IP Information with cURL

Execute:

```bash
curl ipinfo.io/45.33.32.156
```

The IPinfo service can return information such as:

- IP address
- Hostname
- City and region
- Country
- Approximate geographic coordinates
- Network organization
- Postal code
- Time zone

The output is returned in JSON format.

### 2. Explore DMitry

Execute:

```bash
/bin/dmitry google.com
```

DMitry (Deepmagic Information Gathering Tool) can collect available domain and host information, including DNS and WHOIS-related information and TCP port scanning results.

### 3. Save the Results to a File

Execute:

```bash
dmitry -wise -o dmitry.txt google.com
```

The command saves the collected information in:

```text
/home/aluno/dmitry.txt
```

The contents of the generated file should then be inspected.

## Technical Analysis

cURL provides command-line access to web resources and APIs.

In this activity, it is used to retrieve IP intelligence data from IPinfo.

DMitry consolidates multiple reconnaissance capabilities into a command-line tool, allowing the collection of information associated with a target domain.

## Result

The activity introduces IP intelligence retrieval, domain reconnaissance, and saving investigation output for later analysis.

## Concepts Practiced

- HTTP requests with cURL
- IP intelligence
- JSON response interpretation
- WHOIS information gathering
- Domain reconnaissance
- Saving investigation results to files

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
