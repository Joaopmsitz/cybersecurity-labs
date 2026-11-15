# Activity 1.2 — Port Scanner using Python Sockets

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Documented

## Objective

Develop a basic TCP port scanner using Python sockets to identify open ports on a target host.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Language | Python 3 |
| Library | socket |
| Target | scanme.nmap.org |
| Target IPv4 | 45.33.32.156 |
| Port Range | 70–80 |

## Procedure

### 1. Create the Scanner

Open the editor:

```bash
nano atividade2.py
```

The provided Python script uses:

- `gethostbyname()` to resolve the target hostname.
- `socket()` to create TCP sockets.
- `connect_ex()` to test whether a connection can be established.
- `time.time()` to measure execution time.

### 2. Execute the Scanner

Run:

```bash
python3 atividade2.py
```

The script tests the target ports and reports those accepting TCP connections.

## Technical Analysis

The supplied script uses:

```python
for i in range(70, 81):
```

Python's `range()` excludes the final value. Therefore, the actual scanned range is 70 through 80, inclusive, despite the broader interval described in the assignment text.

The exercise material describes port 80 as an open port in the expected result.

## Result

The activity demonstrates how a Python socket can test TCP connectivity across a defined range of ports.

The actual output should be interpreted from the corresponding terminal evidence.

## Authorization and Responsible Use

The original exercise identifies scanme.nmap.org as a test environment authorized for learning and limited scanning.

Port scanning must only be performed against systems for which explicit authorization exists.

## Concepts Practiced

- TCP port scanning
- Socket programming
- Hostname resolution
- Open port identification
- Connection testing
- Basic network reconnaissance

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
