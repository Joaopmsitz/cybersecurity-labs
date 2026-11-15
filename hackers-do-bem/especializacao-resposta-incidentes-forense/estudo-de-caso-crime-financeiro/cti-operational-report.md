# CTI Operational Report — Good Money Financial

> **Program:** Hackers do Bem  
> **Case:** Financial Crime — Network Incident Investigation  
> **Student:** João Paulo Moreira de Sousa  
> **Discipline:** Computer Forensics and Incident Response  
> **Institution:** Hackers do Bem  
> **Instructor:** Armellini Alexandre  
> **Analysis Tool:** Zeek and `zeek-cut`

## 1. Executive Summary

Good Money Financial reported a security incident involving a compromised Windows server and suspected exposure of sensitive customer information.

The network investigation used Zeek logs generated from the supplied PCAP to identify the affected client and examine HTTP activity.

The analysis identified a Windows client at `172.17.1.129`, with MAC address `00:1e:67:4a:d7:5c` and hostname `Nalyvaiko-PC`.

The HTTP records revealed a URL associated with the download of a Microsoft Word document:

```text
ifcingenieria.cl/QpX8It/BIZ/Firmenkunden/
```

Based on the document download and the malicious delivery chain identified in the course investigation, the incident was classified as a phishing infection involving a malicious document.

The findings provide network indicators that can be used to identify affected systems, support containment, and guide endpoint investigation.

## 2. Scope and Methodology

The analysis was performed on the forensic Linux workstation.

The supplied archive was located in:

```text
/opt/estudodecaso
```

The course-provided extraction command was:

```bash
cd /opt/estudodecaso
sudo unzip -P infected /opt/estudodecaso/2018-CTF-from-malware-traffic-analysis.net-2-of-2.pcap.zip
```

The PCAP was investigated using Zeek-generated logs and the `zeek-cut` utility.

Zeek creates structured logs for network protocols. `zeek-cut` reads the log field headers and outputs selected fields in a chosen order, making it useful for targeted examination of DHCP and HTTP records.

### 2.1 DHCP Analysis

The DHCP log was used to correlate the client's IP address with its hardware address and hostname.

The relevant Zeek fields are:

| Field | Purpose |
|---|---|
| `client_addr` | Client IP address |
| `mac` | Client hardware address |
| `host_name` | Hostname provided by the client |
| `assigned_addr` | Address assigned through DHCP |

The following is a reproducible field-selection example:

```bash
cat dhcp.log | zeek-cut client_addr mac host_name assigned_addr
```

The output can be narrowed to the client of interest:

```bash
cat dhcp.log | zeek-cut client_addr mac host_name assigned_addr | grep '172.17.1.129'
```

These commands illustrate the relevant fields and filtering logic. They are not claimed to be a verbatim transcript of the original terminal session.

### 2.2 HTTP Analysis

The HTTP log was examined to identify the request associated with a Microsoft Word document.

Relevant fields include:

| Field | Purpose |
|---|---|
| `ts` | Event timestamp |
| `id.orig_h` | Request origin address |
| `id.resp_h` | Response destination address |
| `method` | HTTP method |
| `host` | Requested host |
| `uri` | Requested resource path |
| `status_code` | HTTP response status |
| `resp_mime_types` | Response content MIME type |
| `resp_filenames` | Identified response filenames, when available |

A reproducible field-selection example is:

```bash
cat http.log | zeek-cut ts id.orig_h id.resp_h method host uri status_code resp_mime_types resp_filenames
```

The HTTP records can then be reviewed for Microsoft Word-related content types and resource paths.

A simple text search may help narrow the output:

```bash
cat http.log | zeek-cut ts id.orig_h host uri status_code resp_mime_types resp_filenames | grep -Ei 'word|msword|\.docx?'
```

The exact output and matching record should be correlated with the original PCAP and the corresponding Zeek log entry.

## 3. Questions and Findings

### Q1 — What is the MAC address of the Windows client at 172.17.1.129?

**Finding:**

```text
00:1e:67:4a:d7:5c
```

The address was identified through DHCP log analysis.

The DHCP record associated the client IP address with the corresponding MAC address.

**Evidence:** PDF page 7.

### Q2 — What is the hostname of the Windows client at 172.17.1.129?

**Finding:**

```text
Nalyvaiko-PC
```

The hostname was identified in the DHCP log information associated with the investigated client.

**Evidence:** PDF page 8.

### Q3 — Which URL in the PCAP returned a Microsoft Word document?

**Finding:**

```text
ifcingenieria.cl/QpX8It/BIZ/Firmenkunden/
```

The URL was identified through HTTP log analysis and the response associated with a Microsoft Word document.

The URL is preserved in the exact form provided in the investigation report. The protocol scheme was not separately recorded in the supplied answer.

**Evidence:** PDF page 9.

### Q4 — What type of infection occurred in the PCAP?

**Finding:**

```text
Phishing
```

The incident was classified as phishing involving delivery of a malicious Microsoft Word document and a subsequent malicious payload.

## 4. Indicators of Compromise

The following indicators were identified during the network investigation.

| Type | Indicator | Description |
|---|---|---|
| IPv4 Address | `172.17.1.129` | Affected Windows client |
| MAC Address | `00:1e:67:4a:d7:5c` | Hardware address associated with the client |
| Hostname | `Nalyvaiko-PC` | Windows client hostname |
| Domain | `ifcingenieria.cl` | Host associated with the suspicious download URL |
| URL Path | `/QpX8It/BIZ/Firmenkunden/` | Resource path associated with the Microsoft Word download |
| Full URL as Reported | `ifcingenieria.cl/QpX8It/BIZ/Firmenkunden/` | URL identified in the HTTP analysis |
| File Type | Microsoft Word document (`.doc`) | Document associated with the infection chain |
| Protocol | HTTP | Protocol used in the observed download |

The supplied report did not include a file hash, a confirmed payload hash, or a complete set of command-and-control IP addresses. These values are therefore not added as confirmed IoCs.

## 5. Incident Assessment

The network evidence indicates that the Windows client `Nalyvaiko-PC` at `172.17.1.129` accessed a URL associated with a Microsoft Word document.

The document was identified as part of a phishing infection chain involving malicious payload delivery.

The correlation of the DHCP and HTTP records provides the following context:

1. DHCP records associate the IP address with the MAC address and hostname.
2. HTTP records identify the requested resource.
3. The response information associates the URL with a Microsoft Word document.
4. The malicious document and observed delivery chain support the phishing classification.

The findings establish a network-based lead for identifying the affected endpoint and guiding further host investigation.

The PCAP findings alone do not establish every subsequent action performed on the endpoint or prove the full extent of data exposure.

## 6. Recommendations

### 6.1 Containment

- Isolate the endpoint `172.17.1.129` from the corporate network while preserving forensic evidence.
- Block or restrict access to the suspicious domain and URL path after validating whether the domain has any legitimate business use.
- Identify other endpoints that contacted the same domain or requested the same resource.
- Preserve the original PCAP and Zeek logs for further analysis.

### 6.2 Endpoint Investigation

- Examine the downloaded Word document and its associated files.
- Search the endpoint for suspicious child processes and files created after the document download.
- Review persistence mechanisms, scheduled tasks, startup entries, and unusual registry changes.
- Search for additional indicators derived from the recovered document and payload.
- Acquire a forensic image if the endpoint remains available for investigation.

### 6.3 Credential and Account Protection

- Assess whether credentials may have been exposed.
- Reset credentials for affected users when there is evidence or a reasonable risk of compromise.
- Review authentication activity for unusual logons and access attempts.
- Enforce multi-factor authentication for relevant accounts.

### 6.4 Network Monitoring

- Search DNS, proxy, firewall, and HTTP logs for additional requests to the suspicious domain.
- Monitor for communication with infrastructure identified during endpoint analysis.
- Review outbound traffic for unusual destinations and patterns.
- Correlate endpoint, network, and authentication telemetry.

### 6.5 Recovery and Remediation

- Remove confirmed malicious files and persistence mechanisms.
- Rebuild the affected endpoint if system integrity cannot be established.
- Apply operating system and application security updates.
- Strengthen email filtering and attachment inspection.
- Provide targeted phishing awareness training.
- Document the incident timeline and lessons learned.

## 7. Conclusion

The Zeek analysis identified the Windows client involved in the incident and the URL associated with the Microsoft Word document download.

The client was identified as:

```text
IP:       172.17.1.129
MAC:      00:1e:67:4a:d7:5c
Hostname: Nalyvaiko-PC
```

The suspicious resource was:

```text
ifcingenieria.cl/QpX8It/BIZ/Firmenkunden/
```

The incident was classified as phishing involving malicious document delivery.

The identified indicators can be used for endpoint isolation, threat hunting, domain blocking, credential review, and further incident investigation.

## 8. Evidence

| Question | Evidence |
|---|---|
| Q1 — MAC Address | PDF page 7 |
| Q2 — Hostname | PDF page 8 |
| Q3 — Microsoft Word URL | PDF page 9 |
| Q4 — Infection Type | Written finding: Phishing |
| Q5 — Operational CTI Report | This document |

[View Consolidated Evidence](./evidences.pdf)

## References

- [Zeek — Log Formats and Inspection](https://docs.zeek.org/en/current/log-formats.html)
- [Zeek — DHCP Log Fields](https://docs.zeek.org/en/current/reference/logs/dhcp.html)
- [Zeek — HTTP Log Fields](https://docs.zeek.org/en/current/reference/logs/http.html)
- [Zeek — Files Log Fields](https://docs.zeek.org/en/current/reference/logs/files.html)
- [Zeek Auxiliary Programs — zeek-cut](https://github.com/zeek/zeek-aux)
- [NIST — Computer Security Incident Handling Guide](https://csrc.nist.gov/pubs/sp/800/61/r2/final)

---

[Back to Case Overview](./README.md)
