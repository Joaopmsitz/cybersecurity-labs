# Phishing Mail - Malicious ZIP Attachment

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 82 |
| Detection Rule | SOC140 - Phishing Mail Detected - Suspicious Task Scheduler |
| Event Time | 2021-03-21 12:26 |
| Category | Phishing |
| Sender | aaronluo@cmail.carleton.ca |
| Recipient | mark@letsdefend.io |
| SMTP IP | 189.162.189.159 |
| Subject | COVID19 Vaccine |
| Attachment | Password-protected ZIP |
| Device Action | Blocked |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

The alert was generated after a phishing email using a COVID-19 vaccine-themed lure was identified.

The message contained a password-protected ZIP attachment. Investigation confirmed that the archive contained a malicious PDF file.

Email security controls blocked delivery before the attachment reached the recipient's endpoint.

## 3. Evidence Analysis

### Email Analysis

The email used urgency around COVID-19 vaccine information to encourage the recipient to open the attachment.

| Field | Value |
|---|---|
| Sender | aaronluo@cmail.carleton.ca |
| Recipient | mark@letsdefend.io |
| Subject | COVID19 Vaccine |
| SMTP IP | 189.162.189.159 |
| Event Time | 2021-03-21 12:26 |
| Device Action | Blocked |

### Attachment Analysis

The email contained a password-protected ZIP archive.

| Attribute | Value |
|---|---|
| Archive | ZIP |
| Archive MD5 | `72c812cf21909a48eb9cceb9e04b865d` |
| Archive Password | `infected` |
| Extracted File | `Material.pdf` |
| PDF SHA256 | `39fb927c32221134a423760c5d1f58bca4cbbcc87c891c79e390a22b63608eb4` |

Sandbox and threat intelligence analysis classified the attachment as malicious.

A public analysis associated the PDF with attempted communication to `69.39.225.3`. The available investigation records did not identify outbound communication from the recipient's endpoint to this address.

### Delivery and Endpoint Assessment

The email security gateway recorded the message as Blocked.

Consequently:

- The email was not delivered to the recipient.
- No user interaction with the attachment was established.
- No attachment execution on the endpoint was identified.
- No endpoint containment action was required.

### External References

- [Independent EventID 82 analysis](https://medium.com/@higherdas09/letsdefend-soc140-phishing-mail-detected-event-id-82-dc88e1134d7e)
- [SOC140 technical walkthrough](https://darrenkhobbs.com/letsdefend-soc140-phishing-mail-detected-suspicious-task-scheduler/)

These sources corroborate the blocked email, the password-protected archive, and the malicious PDF.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1566.001 | Spearphishing Attachment | Phishing email containing a malicious ZIP attachment |

The alert rule name references Suspicious Task Scheduler. However, the available evidence does not independently establish scheduled task creation or execution.

## 5. Response Actions

- Reviewed sender, recipient, and email metadata.
- Examined the message and its attachment.
- Analyzed the archive and extracted PDF.
- Reviewed sandbox and threat intelligence results.
- Verified that email security blocked delivery.
- Classified the alert as True Positive.

No endpoint isolation or malware removal was required because the email was blocked before delivery.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing attempt involving a password-protected ZIP attachment containing a malicious PDF.

Email security controls blocked the message before delivery, preventing user interaction and endpoint execution.

**Final Verdict: True Positive**

**Impact Assessment: Malicious Attachment Blocked Before Delivery**
