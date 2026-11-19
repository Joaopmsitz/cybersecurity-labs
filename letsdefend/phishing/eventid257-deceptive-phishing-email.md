# Deceptive Phishing Email

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 257 |
| Detection Rule | SOC282 - Phishing Alert - Deceptive Mail Detected |
| Event Time | 2024-05-13 09:22 |
| Severity | Medium |
| Category | Phishing |
| Recipient | Felix |
| Sender | free@coffeeshoop.com |
| SMTP IP | 103.80.134.63 |
| Subject | Free Coffee Voucher |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

A phishing email using a free coffee voucher lure was delivered to the internal user Felix.

The investigation identified a malicious ZIP attachment, execution of `Coffee.exe`, and outbound communication with infrastructure associated with AsyncRAT.

The available public investigation records identify the affected endpoint as Felix (`172.16.20.151`).

## 3. Evidence Analysis

### Email Analysis

| Field | Value |
|---|---|
| Sender | free@coffeeshoop.com |
| Recipient | Felix@letsdefend.io |
| SMTP IP | 103.80.134.63 |
| Subject | Free Coffee Voucher |
| Event Time | 2024-05-13 09:22 |

The original report records the sender domain as `coffeeshoop.com`. An independent writeup spells it `coffeeshooop.com`. The original alert should be used to resolve this spelling discrepancy.

### Payload Analysis

The email contained a ZIP archive:

`free-coffee.zip`

The archive delivered the executable:

`Coffee.exe`

Sandbox analysis identified the executable as **AsyncRAT**, a Remote Access Trojan.

### Network Activity

The investigation identified outbound communication to:

| Field | Value |
|---|---|
| C2 IP | 37.120.233.226 |
| C2 Port | 3451/TCP |

An independent investigation recorded two outbound attempts to the C2 endpoint: one denied and one permitted by the firewall.

The public writeup also records the following timeline:

| Time | Activity |
|---|---|
| 09:20 | Phishing email delivered |
| 09:22 | SOC282 alert generated |
| 12:59 | User accessed the download link |
| 13:00 | `Coffee.exe` executed and C2 communication attempted |

### External References

- [Independent EventID 257 investigation](https://github.com/Avdhut-Gogawale/SOC-Analyst-Writeups/blob/main/Phishing/SOC282-Phishing-AsyncRAT.md)
- [Additional EventID 257 writeup](https://www.policytopackets.com/writeups/letsdefend/soc/282_257/)

These sources provide additional context for the payload, endpoint, and C2 connection.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1566.002 | Spearphishing Link | Phishing email using a malicious download link |
| T1204.001 | User Execution: Malicious Link | User accessed the phishing link |
| T1105 | Ingress Tool Transfer | Malicious ZIP and executable delivery |
| T1071.001 | Application Layer Protocol: Web Protocols | Outbound web communication |

## 5. Response Actions

### Investigation Performed

- Reviewed the phishing email and sender infrastructure.
- Investigated the malicious ZIP attachment.
- Reviewed `Coffee.exe` sandbox classification.
- Correlated user activity with the download and execution timeline.
- Reviewed outbound firewall communication.
- Identified the C2 endpoint and malware family.
- Classified the alert as True Positive.

### Recommended Containment

- Isolate the affected endpoint if not already contained.
- Remove the malicious email and attachment.
- Block validated C2 indicators.
- Investigate persistence and credential theft.
- Hunt for related AsyncRAT indicators across the environment.

The supplied report does not independently confirm that all containment recommendations were completed.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing incident involving delivery and execution of `Coffee.exe`, identified as AsyncRAT.

The affected endpoint communicated with external infrastructure associated with the RAT, including `37.120.233.226:3451`.

The sender-domain spelling discrepancy should be resolved against the original email record before the indicator is finalized.

**Final Verdict: True Positive**

**Classification: Phishing / AsyncRAT Delivery**
