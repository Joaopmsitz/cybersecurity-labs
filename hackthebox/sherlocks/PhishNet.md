# PhishNet — Sherlock (Very Easy)

**Category:** Email Security & Digital Forensics  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/985)

## Overview

PhishNet is a Sherlock challenge focused on phishing email analysis, email forensics, and malicious attachment investigation.

The scenario involves a suspicious email containing phishing indicators and a potentially malicious attachment. The investigation examines email metadata, sender authentication, social engineering techniques, and file characteristics to identify indicators of compromise (IOCs).

## Investigation Focus

- Email header analysis
- SMTP relay investigation
- Sender and Reply-To verification
- SPF authentication result analysis
- Phishing domain identification
- Base64 decoding
- ZIP archive inspection
- Attachment hash calculation using SHA-256
- Malicious file identification
- IOC extraction
- MITRE ATT&CK mapping

## Tools Used

- Linux command-line utilities
- `grep`
- Python
- Base64 decoding
- ExifTool
- Manual email and attachment analysis

## Key Findings

The investigation identified several phishing indicators:

- Sender originating IP address and mail relay information
- Sender and Reply-To email addresses
- SPF authentication results
- A phishing URL associated with the campaign
- A fake company identity used for social engineering
- A malicious ZIP attachment
- The attachment's SHA-256 hash
- A batch script disguised as a PDF through a double-extension filename

The findings demonstrate how email metadata, attachment inspection, and file characteristics can be correlated to assess a suspected phishing attempt.

## MITRE ATT&CK

- **T1566.001 — Spearphishing Attachment**
- **T1204 — User Execution**

## Key Takeaways

- Email headers provide useful evidence for tracing message delivery and validating sender information.
- SPF results are one signal in email authentication analysis and should be evaluated alongside other evidence.
- Double extensions can disguise executable scripts as apparently harmless documents.
- Hashes help identify and correlate suspicious files across investigations.
- Extracting and documenting IOCs supports threat validation and follow-up analysis.

---

[Back to Sherlocks](./README.md) · [Back to Hack The Box](../README.md)
