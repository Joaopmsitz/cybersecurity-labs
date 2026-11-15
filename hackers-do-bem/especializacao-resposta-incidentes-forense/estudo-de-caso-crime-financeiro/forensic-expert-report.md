# Digital Forensic Expert Report — Financial Crime Case

> **Program:** Hackers do Bem  
> **Case:** Financial Crime — Good Money Financial  
> **Student / Examiner:** João Paulo Moreira de Sousa  
> **Discipline:** Computer Forensics and Incident Response  
> **Institution:** Hackers do Bem  
> **Instructor:** Armellini Alexandre  
> **Forensic Tool:** Autopsy  
> **Evidence Type:** Segmented forensic disk image  
> **Status:** Completed

## 1. Introduction

This forensic expert report documents the examination of a notebook seized during an investigation conducted by the Cybercrime Police Department (DCC).

The investigation concerns a security incident affecting Good Money Financial, in which a server was compromised and sensitive customer information may have been exposed.

Following the initial incident response investigation, the company reported the incident to the DCC.

The case narrative states that information provided to the internet service provider associated an IP address and port with Greg Schardt, who became a person of interest.

A notebook allegedly used in the investigated activities was seized and submitted for forensic examination.

The main objective of this examination was to analyze the disk image, verify its integrity, identify system and user information, inspect potentially relevant applications and deleted files, and reconstruct the available activity timeline.

The examination was conducted using Autopsy and the segmented forensic image supplied through the course material.

## 2. Methodology

### 2.1 Forensic Approach

The investigation followed a structured digital forensic examination process:

1. Identify and obtain all segments of the forensic disk image.
2. Preserve the original evidence and perform the analysis against the acquired image.
3. Verify the available MD5 hash against the reference value.
4. Add the segmented image to an Autopsy case.
5. Examine operating system and registry artifacts.
6. Identify the registered owner and computer identity.
7. Examine user and logon information.
8. Review installed applications.
9. Examine Recycle Bin artifacts and logical deletion evidence.
10. Review available timestamps and reconstruct the timeline.
11. Document findings and limitations.

The examination focused on the evidence supplied with the case and the questions defined by the practical exercise.

### 2.2 Forensic Application

The primary forensic application was:

```text
Autopsy
```

Autopsy was used to add and examine the segmented disk image, browse filesystem artifacts, review operating system information, identify user records, inspect installed applications, and examine the available timeline and deleted-file artifacts.

The exact Autopsy version was not included in the submitted report.

### 2.3 Evidence Integrity

The forensic image was supplied with the following MD5 reference:

```text
aee4fcd9301c03b3b054623ca261959a
```

The MD5 value obtained during the examination was reported as matching the reference value.

The match supports the conclusion that the examined image corresponded to the supplied reference evidence.

MD5 is preserved here because it was the hash algorithm specified by the case. For new evidence acquisitions, an additional modern hash such as SHA-256 should also be recorded.

## 3. Description of the Examined Equipment

### 3.1 Device Identification

| Item | Information |
|---|---|
| Device Type | Notebook computer |
| Device Model | Dell Latitude CPi |
| Manufacturer | Dell |
| Forensic Dataset | NIST CFReDS Hacking Case |
| Disk Image Format | E01/E02 |
| Operating System | Microsoft Windows XP |
| Registered Owner | Greg Schardt |
| Computer Name | `N-1A9ODN6ZXK4LQ` |
| Last Logged-On User | `Mr. Evil` |
| Serial Number | Not recorded in the submitted examination report |

The Dell Latitude CPi identification is based on the forensic image dataset supplied for the exercise.

The serial number was not recorded in the available student report and is therefore not asserted here.

### 3.2 Evidence Files

The forensic image was provided as a segmented image set.

The course instructions identified the first part in:

```text
C:\curso\estudodecaso
```

The second segment was obtained from the CFReDS archive:

```text
4Dell Latitude CPi.E02
```

Download source:

```text
https://cfreds-archive.nist.gov/images/4Dell%20Latitude%20CPi.E02
```

Both image segments were placed in the same directory before the image was added to Autopsy.

### 3.3 Hash Information

| Hash Type | Value |
|---|---|
| MD5 Reference | `aee4fcd9301c03b3b054623ca261959a` |
| MD5 Examined Image | `aee4fcd9301c03b3b054623ca261959a` |
| Comparison | Match |
| Integrity Finding | Consistent with the supplied reference value |

### 3.4 Origin and Custody Context

According to the case narrative, the notebook was found in Greg Schardt's possession during a search and seizure conducted as part of the investigation.

The device was subsequently submitted for forensic examination.

The exact seizure date, time, physical address, collecting officer identification, and evidence custody record were not included in the supplied student report.

These missing acquisition details are not inferred or fabricated in this document.

## 4. Collection of Evidence

The investigation considered the following sources:

| Evidence Source | Purpose |
|---|---|
| Segmented E01/E02 image | Primary disk evidence |
| MD5 metadata | Integrity comparison |
| Windows operating system artifacts | Identification of the installed system |
| Windows registry | Registered owner, computer name, and shutdown information |
| SAM and user artifacts | Account and logon information |
| Installed application records | Identification of potentially relevant utilities |
| Recycle Bin artifacts | Identification of logically deleted files |
| Filesystem metadata | Support for timeline reconstruction |
| Autopsy results | Centralized examination and evidence review |

### 4.1 Adding the Image to Autopsy

Autopsy was used to create a forensic case and add the disk image as a data source.

The first segment of the image was selected from:

```text
C:\curso\estudodecaso
```

The E02 segment was placed in the same folder as required by the course instructions.

Autopsy supports segmented forensic image formats and can use the additional image segments when they are available to the case.

The image was then processed using the configured examination and ingest operations.

### 4.2 System and Registry Examination

The operating system and registry artifacts were examined to identify:

- Operating system version.
- Registered owner.
- Computer name.
- User information.
- Logon details.
- Last recorded system shutdown.

Relevant Windows artifacts include registry hives such as:

```text
C:\WINDOWS\system32\config\SOFTWARE
C:\WINDOWS\system32\config\SYSTEM
C:\WINDOWS\system32\config\SAM
```

The corresponding registry information was used to answer the system identity questions.

### 4.3 Installed Software Examination

Installed applications were reviewed to identify tools that may be relevant to network discovery, credential handling, traffic capture, or other security-related activities.

The presence of these applications was documented as an investigative finding.

Installation alone does not prove that an application was used to perform the alleged crime. Evidence of execution and associated activity would be required for a stronger attribution.

### 4.4 Recycle Bin Examination

The Recycle Bin artifacts were examined to determine whether deleted files were still recoverable.

The findings indicated that files were present in the Recycle Bin and had been logically deleted rather than securely erased from the media.

The supplied report did not include the exact filenames or a complete listing of the recovered files.

## 5. Analysis and Results

## Q6 — Evidence Integrity and Operating System

### Q6(a) — Is the received disk image intact?

**Finding: Yes.**

The MD5 value obtained during the examination matched the supplied reference value:

```text
Reference MD5: aee4fcd9301c03b3b054623ca261959a
Examined MD5:  aee4fcd9301c03b3b054623ca261959a
```

The matching values support the integrity of the examined image relative to the supplied reference.

**Evidence:** PDF page 10.

### Q6(b) — Which operating system was installed?

**Finding:**

```text
Microsoft Windows XP
```

The operating system was identified through the Autopsy examination of the disk image and its system artifacts.

**Evidence:** PDF page 11.

## Q7 — System and User Identification

### Q7(a) — Who is the registered owner?

**Finding:**

```text
Greg Schardt
```

The registered owner information was identified in the Windows system information and registry artifacts.

Relevant registry location:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\RegisteredOwner
```

**Evidence:** PDF page 12.

### Q7(b) — What is the computer account name?

**Finding:**

```text
N-1A9ODN6ZXK4LQ
```

This value was recorded as the computer name in the submitted Autopsy findings.

It identifies the examined system, while `Mr. Evil` is the user account identified separately in the logon analysis.

**Evidence:** PDF page 13.

### Q7(c) — When was the last recorded computer shutdown?

**Finding:**

```text
27 August 2004 — 10:46:27
```

The shutdown time was identified through Windows system artifacts.

The timezone was not specified in the submitted answer, so the timestamp is preserved as originally reported without conversion.

A relevant registry artifact for this type of examination is:

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Windows\ShutdownTime
```

**Evidence:** PDF page 14.

### Q7(d) — Who was the last user to log on?

**Finding:**

```text
Mr. Evil
```

The account was identified as the last user reported to have logged on to the computer.

**Evidence:** PDF page 15.

## Q8 — Installed Programs and Deleted Files

### Q8(a) — Were programs installed that could be used for malicious purposes?

**Finding: Yes.**

The examination identified the following programs:

| Program | Potential Relevance |
|---|---|
| Cain | Network and credential auditing capabilities |
| Look@LAN | Network discovery and monitoring |
| Network Stumbler | Wireless network discovery |
| mIRC | Internet Relay Chat communication |
| Ethereal | Network packet capture and analysis |
| 123WASP | Password recovery or credential-related utility, as identified in the course report |

These applications may have legitimate administrative, diagnostic, or security-testing uses.

Their presence on the examined system is relevant to the investigation, but installation alone does not establish malicious intent or prove that they were used during the incident.

Execution artifacts, configuration files, logs, and related user activity should be correlated before making stronger conclusions.

**Evidence:** PDF pages 16–21.

### Q8(b) — Were there files in the Recycle Bin, and were they permanently deleted?

**Finding: Yes, files were identified in the Recycle Bin.**

The examination indicated that the files had undergone logical deletion but remained recoverable through forensic analysis.

Logical deletion generally removes or changes the filesystem references to a file without immediately overwriting the underlying data content.

The recovered artifacts therefore indicated that deletion had not necessarily resulted in permanent data elimination.

The exact filenames and individual file metadata were not included in the submitted answer.

**Evidence:** PDF page 22.

## 6. Q9 — Evidence Timeline

The disk image analysis provided a partial reconstruction of the system's history and usage.

The following timeline summarizes the findings that were available in the submitted report.

| Sequence | Event or Finding | Timestamp |
|---|---|---|
| 1 | Windows XP was present on the examined notebook | Exact installation timestamp not included in the submitted findings |
| 2 | System registration identified Greg Schardt as the registered owner | Registry artifact; exact modification time not supplied |
| 3 | Computer identity was recorded as `N-1A9ODN6ZXK4LQ` | Exact timestamp not supplied |
| 4 | Potentially relevant applications were identified: Cain, Look@LAN, Network Stumbler, mIRC, Ethereal, and 123WASP | Individual installation and execution timestamps not supplied |
| 5 | The last logged-on user was identified as `Mr. Evil` | Exact logon timestamp not included in the submitted answer |
| 6 | Logically deleted files were identified in the Recycle Bin and remained recoverable | Individual deletion timestamps not supplied |
| 7 | Last recorded computer shutdown | **27 August 2004, 10:46:27** |

### Timeline Interpretation

The artifacts establish several important facts about the examined device:

- The system used Microsoft Windows XP.
- The registered owner was Greg Schardt.
- The computer name was `N-1A9ODN6ZXK4LQ`.
- The last reported user was `Mr. Evil`.
- Several network and security-related applications were installed.
- The Recycle Bin contained logically deleted files that remained recoverable.
- The last recorded shutdown occurred on 27 August 2004 at 10:46:27, as reported in the examination.

The submitted findings do not provide individual timestamps for all installed programs, user activity, and deleted files.

For that reason, this is a partial evidence timeline rather than a complete event-by-event reconstruction.

A complete timeline would require the original Autopsy Timeline export and the individual timestamps associated with the recovered artifacts.

## 7. Q10 — Discussion and Conclusions

### 7.1 Introduction

This report documents the forensic examination of a notebook associated with the Good Money Financial investigation.

The device was reportedly seized during an operation conducted by the Cybercrime Police Department.

The case identifies Greg Schardt as the person associated with the examined notebook and investigates whether the device contains artifacts relevant to the alleged cybercrime.

The examination used the supplied segmented disk image and Autopsy to identify system information, user information, installed applications, deleted files, and timeline artifacts.

### 7.2 Method

The forensic examination used Autopsy to analyze the supplied disk image.

The procedures included:

- Locating both image segments.
- Adding the disk image to an Autopsy case.
- Comparing the calculated MD5 value with the supplied reference.
- Identifying the Windows operating system.
- Reviewing operating system and registry artifacts.
- Identifying the registered owner and computer name.
- Examining account and logon information.
- Reviewing installed applications.
- Examining the Recycle Bin.
- Correlating available timestamps and preparing a timeline.

The examination was based on the supplied evidence and the results recorded in the submitted screenshots and report.

### 7.3 Equipment Description

| Attribute | Finding |
|---|---|
| Device Type | Notebook |
| Manufacturer | Dell |
| Model | Latitude CPi |
| Operating System | Microsoft Windows XP |
| Image Format | E01/E02 |
| Registered Owner | Greg Schardt |
| Computer Name | `N-1A9ODN6ZXK4LQ` |
| Last Logged-On User | `Mr. Evil` |
| Serial Number | Not recorded in the submitted report |
| Reference MD5 | `aee4fcd9301c03b3b054623ca261959a` |

The notebook was described in the case narrative as having been seized from Greg Schardt's possession.

The exact seizure location and collection time were not provided in the available documentation.

### 7.4 Collection of Evidence

The examination considered the following evidence:

- Segmented forensic disk image.
- Supplied MD5 reference value.
- Windows XP operating system artifacts.
- Registry information.
- User and logon information.
- Installed application records.
- Recycle Bin artifacts.
- Filesystem metadata.
- Autopsy timeline information.

### 7.5 Analysis and Results

The MD5 comparison confirmed that the examined image matched the supplied reference value:

```text
aee4fcd9301c03b3b054623ca261959a
```

The system was identified as Microsoft Windows XP.

The registered owner was:

```text
Greg Schardt
```

The computer name was:

```text
N-1A9ODN6ZXK4LQ
```

The last reported user to log on was:

```text
Mr. Evil
```

The last recorded shutdown was:

```text
27 August 2004 at 10:46:27
```

The analysis also identified several applications with potential relevance to security and network activity:

- Cain
- Look@LAN
- Network Stumbler
- mIRC
- Ethereal
- 123WASP

The examination of the Recycle Bin identified logically deleted files that remained recoverable.

These findings provide information about the system identity, software environment, and user activity.

### 7.6 Discussion

The examination identified artifacts that are relevant to the investigation.

The registered owner information links the operating system registration to Greg Schardt.

The computer identity and user information provide further context for the examined notebook.

The installation of network discovery, packet analysis, and credential-related utilities is relevant because these applications may support activities involving network reconnaissance, traffic inspection, and credential analysis.

However, the presence of these utilities must not be treated as conclusive proof of criminal activity.

A stronger finding would require evidence demonstrating execution, configuration, or use of the applications during the period under investigation.

The Recycle Bin findings demonstrate that deleted content remained recoverable through forensic examination.

This is relevant to the reconstruction of user activity and the identification of files that may have been intentionally removed from normal filesystem access.

### 7.7 Conclusions

The forensic image examination produced the following conclusions:

1. The examined image's MD5 value matched the supplied reference value.
2. The system used Microsoft Windows XP.
3. The registered owner was Greg Schardt.
4. The computer name was `N-1A9ODN6ZXK4LQ`.
5. The last reported user to log on was `Mr. Evil`.
6. The last recorded shutdown was 27 August 2004 at 10:46:27.
7. Several dual-use network and security-related applications were installed.
8. Logically deleted files were present in the Recycle Bin and remained recoverable.

The findings provide relevant information that can support the investigation and correlate the seized notebook with the case narrative.

They should be interpreted together with the network evidence, system artifacts, and any additional forensic information obtained during the investigation.

The findings do not, by themselves, establish the exact actions performed by every identified application or prove that every installed tool was used in the alleged incident.

### 7.8 Recommendations

For a complete forensic investigation, the following additional actions are recommended:

- Preserve the original image and maintain a documented chain of custody.
- Record an additional SHA-256 hash for the evidence.
- Export the complete Autopsy timeline with timestamps and timezone information.
- Record the exact filenames and metadata of the recovered deleted files.
- Examine application execution artifacts, configuration files, and related user activity.
- Correlate the computer's user artifacts with the Zeek network indicators.
- Preserve all original logs and evidence exports.
- Document the exact collection and seizure details when available.

## 8. Final Assessment

The network and disk investigations provide complementary findings.

The Zeek analysis identified an affected Windows client and a URL associated with a malicious Microsoft Word document. The disk image investigation identified the Windows operating system, registered owner, computer name, last logged-on user, installed applications, and recoverable deleted files.

Together, these findings support the incident assessment and demonstrate the value of combining network forensics with disk forensics.

The investigation also highlights the importance of evidence integrity, clear documentation, careful interpretation of dual-use tools, and a timeline that distinguishes confirmed timestamps from events whose exact times were not available.

## 9. Evidence and Annexes

| Question | Evidence | PDF Page |
|---|---|---:|
| Q1 | Client MAC address | 7 |
| Q2 | Client hostname | 8 |
| Q3 | Microsoft Word document URL | 9 |
| Q6(a) | MD5 integrity comparison | 10 |
| Q6(b) | Windows XP identification | 11 |
| Q7(a) | Registered owner | 12 |
| Q7(b) | Computer name | 13 |
| Q7(c) | Last shutdown | 14 |
| Q7(d) | Last logged-on user | 15 |
| Q8(a) | Installed applications | 16–21 |
| Q8(b) | Recycle Bin artifacts | 22 |
| Q9 | Evidence timeline | This report |
| Q10 | Forensic expert report | This report |

[View Consolidated Evidence PDF](./evidences.pdf)

## References

- [NIST — Computer Forensics Reference Data Sets (CFReDS)](https://cfreds.nist.gov/)
- [NIST CFReDS — Hacking Case](https://cfreds-archive.nist.gov/Hacking_Case.html)
- [CFReDS — Dell Latitude CPi E02 Image](https://cfreds-archive.nist.gov/images/4Dell%20Latitude%20CPi.E02)
- [Autopsy — User Documentation](https://www.sleuthkit.org/autopsy/docs/user-docs/4.20.0/)
- [Autopsy — Data Sources](https://www.sleuthkit.org/autopsy/docs/user-docs/4.20.0/ds_page.html)
- [Autopsy — Timeline](https://sleuthkit.org/autopsy/docs/user-docs/4.20.0/timeline_page.html)
- [The Sleuth Kit — Official Project](https://www.sleuthkit.org/)

---

[Back to Case Overview](./README.md) · [CTI Operational Report](./cti-operational-report.md)
