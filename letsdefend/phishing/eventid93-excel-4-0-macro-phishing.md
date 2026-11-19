# Excel 4.0 Macro Phishing

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 93 |
| Detection Rule | SOC146 - Phishing Mail Detected - Excel 4.0 Macros |
| Event Time | 2021-06-13 14:13 |
| Severity | High |
| Category | Phishing |
| Sender | trenton@tritowncomputers.com |
| Recipient | lars@letsdefend.io |
| SMTP IP | 24.213.228.54 |
| Subject | RE: Meeting Notes |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

A phishing alert was generated after an email containing an Excel 4.0 Macro attachment was delivered to an internal user.

The investigation focused on validating the attachment, analyzing endpoint activity, and determining whether malicious code execution occurred.

Analysis identified macro-related activity, suspicious DLL execution through `regsvr32.exe`, and external communication.

## 3. Evidence Analysis

### Email and Attachment

| Field | Value |
|---|---|
| Sender | trenton@tritowncomputers.com |
| Recipient | lars@letsdefend.io |
| Subject | RE: Meeting Notes |
| SMTP IP | 24.213.228.54 |
| Device Action | Allowed |
| Attachment Hash (MD5) | `11f44531fb088d31307d87b01e8eabff` |

The available analysis associated the email with a malicious Excel 4.0 Macro attachment.

### Endpoint Activity

The independent investigation associated the recipient with the endpoint `LarsPRD` (`172.16.17.57`).

The following commands were observed:

```cmd
whoami
ipconfig /all
dir
regsvr32.exe -s ../iroto.dll
regsvr32.exe -s ../iroto1.dll
```

The `regsvr32.exe` commands indicate DLL registration/execution activity involving `iroto.dll` and `iroto1.dll`.

Sandbox analysis and endpoint telemetry were recorded as confirming malicious behavior and DLL activity.

### Indicators of Compromise

| Type | Indicator |
|---|---|
| Sender | trenton@tritowncomputers.com |
| Subject | RE: Meeting Notes |
| SMTP IP | 24.213.228.54 |
| Attachment MD5 | `11f44531fb088d31307d87b01e8eabff` |
| Process | `regsvr32.exe` |
| DLL | `iroto.dll` |
| DLL | `iroto1.dll` |

### External Reference

[Independent SOC146 investigation](https://github.com/topsoftrees/LetsDefend/blob/main/SOC146%20-%20Phishing%20Mail%20Detected.md)

The independent report provides additional context for the endpoint association and malicious attachment analysis.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1566.001 | Spearphishing Attachment | Phishing email with a malicious attachment |
| T1204.002 | User Execution: Malicious File | Malicious attachment execution |
| T1218.010 | System Binary Proxy Execution: Regsvr32 | `regsvr32.exe` used with suspicious DLLs |
| T1082 | System Information Discovery | `ipconfig /all` |

## 5. Response Actions

- Reviewed the phishing email and metadata.
- Analyzed the malicious attachment.
- Reviewed sandbox results.
- Investigated endpoint process activity.
- Identified suspicious DLL execution.
- Reviewed external communication indicators.
- Collected indicators of compromise.
- Recorded endpoint containment in the original investigation.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing incident involving a malicious Excel 4.0 Macro attachment.

Endpoint activity included reconnaissance commands and suspicious DLL execution through `regsvr32.exe`. The evidence supported malicious execution and compromise of the affected endpoint.

**Final Verdict: True Positive**

**Classification: Phishing Email / Excel 4.0 Macro Execution**
