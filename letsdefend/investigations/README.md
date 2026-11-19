# LetsDefend - Investigation Catalog

Central index of SOC investigation reports completed in the LetsDefend training environment.

Each case is identified by its Event ID. SOC identifiers refer to detection rules and may recur across different events.

## Documented Investigation Inventory

| Category | Reports |
|---|---:|
| [Brute Force Investigations](./brute-force/README.md) | 1 |
| [Malware Investigations](./malware/README.md) | 6 |
| [Phishing Investigations](./phishing/README.md) | 7 |
| [Web Attack Investigations](./web-attacks/README.md) | 2 |

**Total: 16 documented investigation reports.**

## Case Index

| Event ID | Category | Detection Rule | Alert / Case |
|---:|---|---|---|
| 17 | malware | SOC106 | [Found Suspicious File - TI Data](./malware/eventid17-found-suspicious-file-ti-data.md) |
| 21 | malware | SOC104 | [Malware Detected](./malware/eventid21-malware-detected.md) |
| 45 | phishing | SOC114 | [SOC114 — Malicious Attachment Detected - Phishing Alert](./phishing/eventid45-malicious-attachment-detected-phishing-alert.md) |
| 52 | phishing | SOC120 | [SOC120 — Phishing Mail Detected - Internal to Internal](./phishing/eventid52-phishing-mail-detected-internal-to-internal.md) |
| 76 | malware | SOC137 | [Malicious File/Script Download Attempt](./malware/eventid76-malicious-file-script-download-attempt.md) |
| 77 | malware | SOC138 | [Suspicious XLS File Execution](./malware/eventid77-suspicious-xls-file-detection.md) |
| 82 | phishing | SOC140 | [Phishing Mail Detected - Suspicious Task Scheduler](./phishing/eventid82-phishing-malicious-attachment.md) |
| 84 | malware | SOC104 | [Malware Detected](./malware/eventid84-malware-detected.md) |
| 86 | phishing | SOC141 | [Phishing URL Detected](./phishing/eventid86-phishing-url-detected.md) |
| 93 | phishing | SOC146 | [Phishing Mail Detected - Excel 4.0 Macros](./phishing/eventid93-phishing-mail-detected-excel-4-0-macros.md) |
| 115 | web-attacks | SOC165 | [SQL Injection Attempt Detected](./web-attacks/eventid115-sql-injection.md) |
| 116 | web-attacks | SOC166 | [JavaScript Code Detected in URL](./web-attacks/eventid116-javascript-code-detected.md) |
| 231 | malware | SOC205 | [Malicious Macro Execution](./malware/eventid231-malicious-macro-execution.md) |
| 234 | brute-force | SOC176 | [RDP Brute Force Detected](./brute-force/eventid234-rdp-brute-force-detected.md) |
| 257 | phishing | SOC282 | [Phishing Email Detected](./phishing/eventid257-phishing-deceptive-email.md) |
| 316 | phishing | SOC338 | [Lumma Stealer - DLL Side-Loading via Click Fix Phishing](./phishing/eventid316-lumma-stealer-clickfix.md) |

## Investigation Methodology

1. Alert triage and review of detection context.
2. Evidence collection and analysis.
3. Threat intelligence correlation.
4. Validation of observed behavior and impact.
5. Assessment of response actions and recommendations.
6. Evidence-based classification and conclusion.

## Documentation Principles

- Distinguish observed evidence from external intelligence.
- Do not claim execution or compromise without supporting telemetry.
- Separate completed response actions from recommendations.
- External write-ups are contextual references, not proof of actions performed in this lab.

## Scope

These are simulated LetsDefend training scenarios, not real-world incident response engagements.

---

[Back to LetsDefend](../README.md) · [Back to Cybersecurity Portfolio](../../README.md)
