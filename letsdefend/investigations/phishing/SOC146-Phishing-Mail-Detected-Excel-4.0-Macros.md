# 🚨 SOC146 - Phishing Mail Detected - Excel 4.0 Macros

## 📌 Summary

A high-severity phishing alert was generated after a malicious email containing an Excel 4.0 Macro attachment was delivered to an internal user.

The investigation focused on validating the attachment, analyzing endpoint activity, and determining whether the malicious file was executed.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC146 |
| Event ID | 93 |
| Category | Phishing |
| Severity | High |
| Sender | trenton@tritowncomputers.com |
| Recipient | lars@letsdefend.io |
| SMTP IP | 24.213.228.54 |
| Subject | RE: Meeting Notes |
| Device Action | Allowed |

---

## 🔍 Investigation

### Key Findings

- Phishing email successfully delivered
- Password-protected attachment identified
- Excel 4.0 Macro activity detected
- Sandbox analysis confirmed malicious behavior
- Communication with malicious infrastructure confirmed
- Execution of malicious DLL files observed
- Endpoint compromise confirmed
- Host containment performed

### Suspicious Commands

```cmd
whoami
ipconfig /all
dir
regsvr32.exe -s ../iroto.dll
regsvr32.exe -s ../iroto1.dll
```

These commands indicate system reconnaissance activity followed by malicious DLL execution using regsvr32.

---

## 🚨 Impact Assessment

- Malicious phishing email confirmed
- Excel 4.0 Macro execution identified
- Malicious attachment executed
- Command execution observed
- External communication detected
- Endpoint compromise confirmed
- Host containment required

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| Sender | trenton@tritowncomputers.com |
| Subject | RE: Meeting Notes |
| SMTP IP | 24.213.228.54 |
| Attachment Hash | 11f44531fb088d31307d87b01e8eabff |
| Process | regsvr32.exe |
| DLL | iroto.dll |
| DLL | iroto1.dll |
| Technique | Excel 4.0 Macros |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1566.001 | Phishing Attachment |
| T1204.002 | User Execution: Malicious File |
| T1059 | Command and Scripting Interpreter |
| T1218.010 | Regsvr32 |
| T1082 | System Information Discovery |

---

## 🛠️ Response Actions

- Classified alert as True Positive
- Investigated email content
- Analyzed malicious attachment
- Reviewed sandbox analysis results
- Investigated endpoint activity
- Confirmed communication with malicious infrastructure
- Identified Indicators of Compromise (IOCs)
- Contained the affected endpoint

---

## 📚 Conclusion

The investigation confirmed a phishing attack involving a malicious Excel 4.0 Macro attachment.

Analysis demonstrated that the attachment was executed, resulting in command execution, malicious DLL activity, and communication with external infrastructure. Evidence confirmed compromise of the affected endpoint and justified immediate containment.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Phishing Email / Malicious Excel 4.0 Macro**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Containment → Documentation**
