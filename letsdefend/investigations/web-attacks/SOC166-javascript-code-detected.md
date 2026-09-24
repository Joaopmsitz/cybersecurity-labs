# 🚨 SOC166 - JavaScript Code Detected in URL

## 📌 Summary

A medium-severity alert was generated after detecting suspicious JavaScript code embedded within a URL, indicating a possible Cross-Site Scripting (XSS) attack attempt against a web application.

The investigation focused on analyzing the malicious payload, validating attack intent, and determining whether code execution was successful.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC166 |
| Category | Web Attack |
| Severity | Medium |
| Attack Type | Cross-Site Scripting (XSS) |

---

## 🔍 Investigation

The investigation began with the analysis of an HTTP request containing a suspicious encoded payload within the URL.

### Key Findings

- Encoded JavaScript was identified in the URL
- The payload was consistent with a Cross-Site Scripting (XSS) attack
- The attacker attempted to inject client-side JavaScript code
- The request targeted a web application input field
- No evidence of successful code execution was identified
- No abnormal application behavior was observed

### Suspicious Payload

```html
<script>alert(1)</script>
```

This payload is commonly used to test whether an application is vulnerable to Cross-Site Scripting by attempting to execute JavaScript code within a user's browser.

---

## 🚨 Impact Assessment

- XSS attack attempt confirmed
- Malicious JavaScript payload identified
- Client-side code execution was attempted
- No evidence of successful exploitation
- No indicators of compromise identified

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| Payload | Encoded JavaScript in URL |
| Technique | Cross-Site Scripting (XSS) |
| Attack Method | JavaScript Injection |
| Target | Web Application Input Field |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1059.007 | JavaScript |
| T1059 | Command and Scripting Interpreter |

---

## 🛠️ Response Actions

- Classified alert as True Positive
- Investigated malicious payload
- Reviewed affected web requests
- Verified no successful code execution occurred
- Recommended input validation controls
- Recommended output encoding and sanitization

---

## 📚 Conclusion

The investigation confirmed a Cross-Site Scripting (XSS) attack attempt involving malicious JavaScript embedded within a URL.

Analysis identified a known JavaScript injection payload designed to execute client-side code. Although the attack attempt was confirmed, no evidence indicated successful execution or compromise of the target application.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Web Attack / Cross-Site Scripting (XSS)**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Response**
