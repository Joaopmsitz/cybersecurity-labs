# Internal Phishing Email

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 52 |
| Detection Rule | SOC120 - Phishing Mail Detected - Internal to Internal |
| Event Time | 2021-02-06 22:24:09 (BRT, as recorded) |
| Category | Exchange / Phishing |
| Sender | john@letsdefend.io |
| Recipient | susie@letsdefend.io |
| SMTP Server | 172.16.20.3 |
| Subject | Meeting |
| Device Action | Allowed |
| Investigation Verdict | False Positive |

## 2. Investigation Overview

The SOC120 rule generated an alert for an email sent between two internal users.

The investigation focused on reviewing the email content, sender and recipient context, SMTP traffic, and available endpoint activity to determine whether the message represented a genuine phishing attempt.

The message was a routine meeting request with no malicious URL, attachment, or credential request.

## 3. Evidence Analysis

### Email Analysis

| Field | Value |
|---|---|
| Sender | john@letsdefend.io |
| Recipient | susie@letsdefend.io |
| Subject | Meeting |
| Sender IP | 172.16.20.3 |

The email content was:

> Hi Susie, Can we arrange a meeting today if you are available?

No malicious URL, attachment, credential request, or suspicious instruction was identified.

### Network Evidence

The email transaction was observed between `JohnComputer` and the internal Exchange server.

```text
Timestamp: 2021-02-06 22:23:51
Source: 172.16.17.82:49582
Destination: 172.16.20.3:25
Protocol: SMTP
```

### Endpoint Investigation

| Field | Value |
|---|---|
| Hostname | JohnComputer |
| IP Address | 172.16.17.82 |
| Domain | LetsDefend |
| Operating System | Windows 10 |
| Primary User | John |

The available browser history included ordinary browsing activity, such as a Google Chrome support page, a Chrome update search, and the LetsDefend GitHub repository.

Command history included:

```text
net user
users
dir /s
dir
ping raw.githubusercontent.com
```

These commands alone do not provide sufficient evidence of compromise or malicious activity.

### Investigation Findings

- Sender and recipient belonged to the same internal domain.
- The message contained a routine meeting request.
- No malicious attachment or URL was identified.
- No credential-harvesting request was found.
- SMTP communication was directed to the internal Exchange server.
- Available browser and command history did not establish malicious activity.

### External Reference

[Independent EventID 52 investigation](https://www.policytopackets.com/writeups/letsdefend/soc/120_52/)

The independent investigation also classified this internal meeting email as a False Positive.

## 4. MITRE ATT&CK Mapping

No MITRE ATT&CK technique was substantiated by the available evidence.

The investigated activity was consistent with legitimate internal email communication.

## 5. Response Actions

- Reviewed the alert and email metadata.
- Inspected the message content.
- Checked for malicious URLs and attachments.
- Reviewed SMTP communication.
- Examined available browser and command history.
- Classified the alert as a False Positive.

No endpoint containment or remediation was required based on the available evidence.

## 6. Conclusion

The investigation determined that the SOC120 alert was a **False Positive**.

The email was a routine internal meeting request between `john@letsdefend.io` and `susie@letsdefend.io`. No malicious links, attachments, credential requests, or other indicators of phishing were identified.

**Final Verdict: False Positive**
