# LetsDefend Investigations

Central index of SOC investigation reports completed in the LetsDefend training environment.

Each case is identified by its Event ID. SOC identifiers refer to detection rules and may recur across different events.

## Documented Investigation Inventory

| Category | Reports |
|---|---:|
| [Brute Force](./brute-force/README.md) | 1 |
| [Malware](./malware/README.md) | 7 |
| [Phishing](./phishing/README.md) | 7 |
| [Web Attacks](./web-attacks/README.md) | 2 |
| **Total** | **17** |

## Case Index

| Event ID | Category | Detection Rule | Investigation |
|---:|---|---|---|
| 17 | Malware | SOC106 | [Suspicious File Detected](./malware/eventid17-suspicious-file-detected.md) |
| 19 | Malware | SOC107 | [Linux Privilege Escalation Exploit Detected](./malware/eventid19-linux-privilege-escalation-detected.md) |
| 21 | Malware | SOC104 | [Emotet Malware Detected](./malware/eventid21-emotet-malware-detected.md) |
| 45 | Phishing | SOC114 | [Malicious Attachment Detected](./phishing/eventid45-malicious-attachment-detected.md) |
| 52 | Phishing | SOC120 | [Internal Phishing Email](./phishing/eventid52-internal-phishing-email.md) |
| 76 | Malware | SOC137 | [Malicious Download Attempt](./malware/eventid76-malicious-download-attempt.md) |
| 77 | Malware | SOC138 | [Suspicious XLS File Detected](./malware/eventid77-suspicious-xls-file-detected.md) |
| 82 | Phishing | SOC140 | [Phishing Mail - Malicious ZIP Attachment](./phishing/eventid82-phishing-malicious-zip-attachment.md) |
| 84 | Malware | SOC104 | [WinRAR Installer - False Positive](./malware/eventid84-winrar-false-positive.md) |
| 86 | Phishing | SOC141 | [Phishing URL Detected](./phishing/eventid86-phishing-url-detected.md) |
| 93 | Phishing | SOC146 | [Excel 4.0 Macro Phishing](./phishing/eventid93-excel-4-0-macro-phishing.md) |
| 115 | Web Attacks | SOC165 | [SQL Injection Attempt](./web-attacks/eventid115-sql-injection-attempt.md) |
| 116 | Web Attacks | SOC166 | [JavaScript Code Detected](./web-attacks/eventid116-javascript-code-detected.md) |
| 231 | Malware | SOC205 | [Malicious Macro Execution](./malware/eventid231-malicious-macro-execution.md) |
| 234 | Brute Force | SOC176 | [RDP Brute Force Detected](./brute-force/eventid234-rdp-brute-force-detected.md) |
| 257 | Phishing | SOC282 | [Deceptive Phishing Email](./phishing/eventid257-deceptive-phishing-email.md) |
| 316 | Phishing | SOC338 | [Lumma Stealer - ClickFix](./phishing/eventid316-lumma-stealer-clickfix.md) |

## Investigation Methodology

1. **Alert Triage** - Review alert metadata, affected assets, and detection context.
2. **Evidence Analysis** - Examine available email, endpoint, network, and system telemetry.
3. **Threat Validation** - Correlate indicators with reputation services and threat intelligence.
4. **Technical Assessment** - Distinguish confirmed activity from assumptions and historical context.
5. **Response Assessment** - Separate completed actions from recommended containment and remediation.
6. **Classification** - Document the verdict and its supporting evidence.

## Documentation Principles

- Conclusions must be supported by evidence.
- Missing telemetry must not be interpreted as proof that an activity did not occur.
- External writeups are references for contextual cross-checking, not evidence collected during the lab.
- MITRE ATT&CK mappings must reflect observed or sufficiently supported behavior.
- Completed response actions must be distinguished from recommendations.
- Platform results and analyst assessments must be documented separately when they differ.

## Scope

These reports document simulated LetsDefend training scenarios. Findings and response actions should not be interpreted as real-world incident response engagements.

---

[Back to Cybersecurity Labs](../README.md)
