# 🚨 SOC140 - Phishing Mail Detected - Suspicious Task Scheduler

## 📌 Summary

A phishing email alert was generated after a malicious email containing a suspicious attachment was delivered to an internal user. The investigation focused on validating the email, analyzing the attachment, and determining whether endpoint compromise occurred.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC140 |
| Event ID | 82 |
| Category | Phishing |
| Sender | aaronluo@cmail.carleton.ca |
| Recipient | mark@letsdefend.io |
| SMTP IP | 189.162.189.159 |
| Subject | COVID19 Vaccine |
| Hostname | MarkPRD |
| User | MarkGuna |

---

## 🔍 Investigation

### Key Findings

- Suspicious phishing email identified
- Malicious attachment included in the email
- Social engineering lure related to COVID-19 news
- Sandbox analysis confirmed malicious behavior
- No evidence of attachment execution on the endpoint
- No malicious network communication observed
- No indicators of endpoint compromise identified

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| SMTP IP | 189.162.189.159 |
| Sender | aaronluo@cmail.carleton.ca |
| Subject | COVID19 Vaccine |
| Attachment Hash | 72c812cf21909a48eb9cceb9e04b865d |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1566 | Phishing |
| T1204 | User Execution |

---

## 🛠️ Response Actions

- Confirmed malicious phishing email
- Validated attachment behavior in sandbox
- Verified no execution occurred on the endpoint
- Reviewed related network activity
- Classified alert as True Positive

---

## 📚 Conclusion

The investigation confirmed that the email contained a malicious attachment and represented a genuine phishing attempt.

Although the attachment was identified as malicious through sandbox analysis, no evidence indicated that the file was executed or that the endpoint was compromised.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Phishing Email / Malicious Attachment**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Response**
