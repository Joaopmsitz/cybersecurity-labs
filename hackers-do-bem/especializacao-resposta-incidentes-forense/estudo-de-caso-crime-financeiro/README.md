# Financial Crime Case Study — Cyber Threat Intelligence and Digital Forensics

> **Program:** Hackers do Bem  
> **Specialization:** Incident Response and Digital Forensics  
> **Case:** Financial Crime — Good Money Financial  
> **Student:** João Paulo Moreira de Sousa  
> **Institution:** Hackers do Bem  
> **Course:** Computer Forensics and Incident Response  
> **Instructor:** Armellini Alexandre  
> **Status:** Completed

## 1. Case Overview

This final practical case combines network traffic investigation, Cyber Threat Intelligence (CTI), and computer forensic analysis.

The scenario involves Good Money Financial, a financial company that experienced a security incident involving a compromised Windows host and suspected exposure of sensitive customer information.

The investigation was divided into two complementary parts:

1. **Incident Response and CTI:** analysis of a PCAP using Zeek and `zeek-cut` to identify the affected Windows client, its network identity, and the URL associated with a malicious Microsoft Word document.
2. **Digital Forensics:** examination of a seized notebook disk image using Autopsy to validate evidence integrity, identify operating system and user artifacts, review installed software and deleted files, and reconstruct the available timeline.

The purpose was to correlate network indicators with artifacts recovered from the disk image and organize the findings into an operational CTI report and a forensic expert report.

## 2. Investigation Environment

### Part 1 — Network Forensics

| Item | Details |
|---|---|
| Forensic Workstation | `forenseLinux` |
| Remote Analysis Host | `192.168.98.10` |
| Network Artifact | PCAP archive |
| Dataset | `2018-CTF-from-malware-traffic-analysis.net-2-of-2.pcap.zip` |
| Network Analysis Tool | Zeek |
| Log Extraction Utility | `zeek-cut` |
| Main Log Sources | `dhcp.log`, `http.log`, and related Zeek logs |

The supplied archive was extracted in:

```text
/opt/estudodecaso
```

The course instructions use the archive password:

```text
infected
```

### Part 2 — Disk Forensics

| Item | Details |
|---|---|
| Forensic Workstation | `forenseWin` |
| Remote Analysis Host | `192.168.98.30` |
| Forensic Application | Autopsy |
| Evidence Dataset | NIST CFReDS Hacking Case |
| Device | Dell Latitude CPi notebook |
| Image Format | E01/E02 segmented forensic image |
| Main Evidence Directory | `C:\curso\estudodecaso` |
| Reference MD5 | `aee4fcd9301c03b3b054623ca261959a` |
| Operating System | Microsoft Windows XP |

The first part of the disk image was supplied in the course environment. The second segment, `4Dell Latitude CPi.E02`, was downloaded from the CFReDS archive and placed in the same directory.

## 3. Case Evidence and Reports

The investigation is documented in the following files:

| File | Description |
|---|---|
| [CTI Operational Report](./cti-operational-report.md) | Network findings, IoCs, incident assessment, and response recommendations |
| [Forensic Expert Report](./forensic-expert-report.md) | Disk image examination, system identity, software artifacts, deleted files, and timeline |
| [Evidence PDF](./evidences.pdf) | Consolidated screenshots and supporting evidence |

## 4. Principal Findings

### Network Investigation

The Zeek analysis identified the Windows client:

| Indicator | Finding |
|---|---|
| IP Address | `172.17.1.129` |
| MAC Address | `00:1e:67:4a:d7:5c` |
| Hostname | `Nalyvaiko-PC` |
| Malicious Document URL | `ifcingenieria.cl/QpX8It/BIZ/Firmenkunden/` |
| Downloaded Content | Microsoft Word document |
| Identified Infection Type | Phishing |

The HTTP analysis identified the URL associated with the Microsoft Word document. The activity was classified as phishing with delivery of a malicious payload.

### Disk Investigation

The Autopsy examination produced the following findings:

| Question | Finding |
|---|---|
| Evidence Integrity | MD5 matched the reference value |
| MD5 | `aee4fcd9301c03b3b054623ca261959a` |
| Operating System | Microsoft Windows XP |
| Registered Owner | Greg Schardt |
| Computer Name | `N-1A9ODN6ZXK4LQ` |
| Last Shutdown | 27 August 2004, 10:46:27 |
| Last Logged-On User | `Mr. Evil` |
| Potentially Relevant Programs | Cain, Look@LAN, Network Stumbler, mIRC, Ethereal, 123WASP |
| Recycle Bin | Logically deleted, recoverable files identified |

The computer name and user account are different artifacts: `N-1A9ODN6ZXK4LQ` identifies the computer, while `Mr. Evil` identifies the last user reported as having logged on.

## 5. Investigation Workflow

The overall investigation followed this sequence:

1. Extract the supplied PCAP archive.
2. Examine Zeek DHCP logs to identify the client MAC address and hostname associated with `172.17.1.129`.
3. Examine Zeek HTTP records to identify the URL that returned a Microsoft Word document.
4. Organize the resulting network findings into an operational CTI report.
5. Obtain the second segment of the forensic disk image.
6. Add the segmented image to an Autopsy case.
7. Verify the disk image MD5 against the supplied reference value.
8. Examine the Windows operating system and registry artifacts.
9. Identify the registered owner, computer name, and last logged-on user.
10. Review installed applications and Recycle Bin artifacts.
11. Correlate the available timestamps and prepare the forensic timeline.
12. Produce the forensic expert report.

## 6. Forensic Considerations and Limitations

The findings are based on the course evidence and the results recorded in the submitted report.

Some acquisition details were not included in the available documentation, such as the notebook's serial number, exact seizure timestamp, exact collection location, and Autopsy version.

The timeline is therefore a partial reconstruction. The exact last shutdown time is documented, but the supplied findings do not provide individual timestamps for every installed application or every deleted file.

The presence of dual-use security and network utilities is relevant to the investigation, but installation alone does not establish that a program was used during the alleged incident.

The complete conclusions and evidence references are documented in the two reports.

## 7. Evidence Mapping

| Evidence | PDF Page |
|---|---:|
| Q1 — Client MAC Address | 7 |
| Q2 — Client Hostname | 8 |
| Q3 — Microsoft Word URL | 9 |
| Q6(a) — Disk Image MD5 | 10 |
| Q6(b) — Operating System | 11 |
| Q7(a) — Registered Owner | 12 |
| Q7(b) — Computer Name | 13 |
| Q7(c) — Last Shutdown | 14 |
| Q7(d) — Last Logged-On User | 15 |
| Q8(a) — Installed Programs | 16–21 |
| Q8(b) — Recycle Bin | 22 |

Q4 and Q5 are documented in the CTI report. Q9 and Q10 are documented in the forensic expert report.

## 8. Conclusion

The case demonstrates how network forensics and disk forensics can complement one another during an incident investigation.

Zeek analysis identified the affected Windows client and a URL associated with a malicious Microsoft Word document. Autopsy examination of the forensic disk image provided information about system identity, user activity, installed programs, deleted files, and the system's recorded shutdown.

The correlation of these evidence sources supports the incident assessment and provides a structured basis for documenting the findings.

The investigation also reinforces the importance of evidence integrity, careful interpretation of artifacts, and distinguishing confirmed findings from assumptions.

## References

- [Zeek — Log Formats and Inspection](https://docs.zeek.org/en/current/log-formats.html)
- [Zeek — DHCP Log Fields](https://docs.zeek.org/en/current/reference/logs/dhcp.html)
- [Zeek — HTTP Log Fields](https://docs.zeek.org/en/current/reference/logs/http.html)
- [Zeek Auxiliary Programs — zeek-cut](https://github.com/zeek/zeek-aux)
- [Autopsy — User Documentation](https://www.sleuthkit.org/autopsy/docs/user-docs/4.20.0/)
- [Autopsy — Data Sources](https://www.sleuthkit.org/autopsy/docs/user-docs/4.20.0/ds_page.html)
- [Autopsy — Timeline](https://sleuthkit.org/autopsy/docs/user-docs/4.20.0/timeline_page.html)
- [NIST — Computer Forensics Reference Data Sets (CFReDS)](https://cfreds.nist.gov/)

---

[Back to the Forensics and Incident Response Specialization](../README.md)
