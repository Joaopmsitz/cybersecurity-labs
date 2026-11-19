# Malicious Attachment Detected

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 45 |
| Detection Rule | SOC114 - Malicious Attachment Detected - Phishing Alert |
| Event Time | 2021-01-31 15:48:30 (UTC+03:00) |
| Severity | High |
| Category | Phishing |
| Sender | accounting@cmail.carleton.ca |
| Recipient | richard@letsdefend.io |
| SMTP IP | 49.234.43.39 |
| Subject | Invoice |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

The investigation focused on a phishing email containing a malicious attachment associated with CVE-2017-11882.

The email was delivered to `richard@letsdefend.io`. Endpoint investigation identified suspicious executable activity on `RichardPRD`, including `JuicyPotato.exe` running with SYSTEM privileges.

The available evidence supports a genuine phishing incident and malicious endpoint activity. However, the exact process lineage between the delivered attachment and `JuicyPotato.exe` was not independently established.

## 3. Evidence Analysis

### Email and Attachment

The email used an invoice-themed lure and contained a suspicious attachment.

| Attribute | Value |
|---|---|
| Subject | Invoice |
| Sender | accounting@cmail.carleton.ca |
| Recipient | richard@letsdefend.io |
| Attachment Type | XLSX |
| File Size | 2.12 MB |
| SHA256 | `44e65a641fb970031c5efed324676b5018803e0a768608d3e186152102615795` |
| VirusTotal | 36/62 detections |
| Associated Vulnerability | CVE-2017-11882 |

The file was associated with exploit and malware-delivery classifications in VirusTotal.

### Endpoint Investigation

The affected endpoint was identified as:

| Field | Value |
|---|---|
| Hostname | RichardPRD |
| IP Address | 172.16.17.45 |
| User | richard |
| Operating System | Windows 10 |
| Domain | letsdefend.local |

The investigation identified `JuicyPotato.exe` at:

`C:\User\Public\JuicyPotato.exe`

The executable was associated with the following analysis results:

| Attribute | Value |
|---|---|
| File | `JuicyPotato.exe` |
| SHA256 | `0f56c703e9b7ddeb90646927bac05a5c6d95308c8e13b88e5d4f4b572423e036` |
| VirusTotal | 57/69 detections |
| Execution Context | `NT AUTHORITY\SYSTEM` |

The executable's reputation and execution context indicate malicious activity with elevated privileges.

The available evidence does not conclusively establish that the phishing attachment directly created or launched `JuicyPotato.exe`.

### External Reference

[Independent EventID 45 investigation](https://www.policytopackets.com/writeups/letsdefend/soc/114_45/)

The external investigation reports that the email was delivered, the attachment was executed, C2 traffic was identified, and endpoint containment was initiated. These actions should be attributed to this report only where they match the original lab records.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1566.001 | Spearphishing Attachment | Phishing email containing a malicious attachment |
| T1204.002 | User Execution: Malicious File | Attachment opening/execution documented in the investigation |

The original alert metadata included T1598.001. The observed email attachment scenario is more directly represented by T1566.001.

## 5. Response Actions

### Investigation Performed

- Reviewed email metadata and attachment details.
- Analyzed the attachment using VirusTotal.
- Reviewed endpoint process activity.
- Investigated `JuicyPotato.exe` and its execution context.
- Collected file hashes and relevant indicators.
- Classified the alert as True Positive.

The original report does not separately document the full containment workflow. An independent writeup for this event records email deletion and endpoint containment initiation.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing incident involving a malicious attachment associated with CVE-2017-11882.

Endpoint analysis also identified `JuicyPotato.exe` running with SYSTEM privileges, providing evidence of malicious activity on the affected host.

Although the phishing attachment and the suspicious executable were identified during the same investigation, their exact execution lineage was not independently established.

**Final Verdict: True Positive**

**Classification: Phishing Attachment / Malicious Endpoint Activity**
