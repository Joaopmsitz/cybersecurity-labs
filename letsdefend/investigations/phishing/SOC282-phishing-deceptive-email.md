# 🚨 SOC282 - Phishing Email Detected

## 📌 Summary

A medium-severity phishing alert was generated after a malicious email containing a weaponized attachment was delivered to an internal user. The investigation focused on email analysis, attachment behavior, endpoint activity, and post-exploitation communication.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC282 |
| Category | Phishing |
| Severity | Medium |
| Recipient | Felix |
| Sender | free@coffeeshoop.com |
| SMTP IP | 103.80.134.63 |
| Subject | Free Coffee Voucher |

---

## 🔍 Investigation

The investigation focused on email metadata, attachment analysis, and endpoint activity.

### Key Findings

- Suspicious sender domain indicating possible spoofing
- Social engineering technique using a "Free Coffee Voucher" lure
- Malicious attachment identified as `free-coffee.zip`
- Attachment contained an executable payload
- Payload execution was confirmed on the target endpoint
- Outbound communication was detected following execution
- Evidence indicated post-infection communication with external infrastructure

---

## 🌐 Network Activity

| Field | Value |
|---------|---------|
| C2 IP | 37.120.233.226 |

The compromised endpoint established outbound communication with an external command-and-control (C2) server following payload execution.

---

## 🚨 Impact Assessment

- Successful phishing email delivery
- Malicious payload execution confirmed
- Endpoint compromise likely
- External C2 communication established
- Increased risk of further malicious activity on the affected host

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| SMTP IP | 103.80.134.63 |
| Domain | coffeeshoop.com |
| Attachment | free-coffee.zip |
| C2 IP | 37.120.233.226 |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1566 | Phishing |
| T1204 | User Execution |
| T1105 | Ingress Tool Transfer |
| T1071 | Application Layer Protocol |

---

## 🛠️ Response Actions

- Classified alert as True Positive
- Recommended isolation of the affected endpoint
- Identified and documented malicious indicators
- Recommended blocking network indicators
- Recommended additional forensic investigation
- Monitored environment for related activity

---

## 📚 Conclusion

The investigation confirmed a phishing attack involving a malicious email attachment designed to deliver malware to the target host.

Analysis identified successful payload execution and outbound communication with an external command-and-control server, indicating likely endpoint compromise.

Based on the collected evidence, the alert was classified as a **True Positive** and required containment and further forensic investigation.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Phishing Email / Malware Delivery**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Impact Assessment → Response**
