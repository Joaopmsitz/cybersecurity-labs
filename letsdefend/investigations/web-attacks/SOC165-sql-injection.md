# 🚨 SOC165 - SQL Injection Attempt Detected

## 📌 Summary

A high-severity alert was generated after detecting suspicious input consistent with a SQL Injection attempt targeting a web application authentication endpoint.

The investigation focused on analyzing HTTP requests, identifying malicious payloads, and determining whether exploitation was successful.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC165 |
| Category | Web Attack |
| Severity | High |
| Attack Type | SQL Injection |

---

## 🔍 Investigation

The investigation began with the analysis of HTTP request logs captured from the affected web application.

### Key Findings

- A malicious SQL Injection payload was identified
- The payload targeted an authentication endpoint
- Multiple repeated requests were observed
- The activity appeared consistent with automated probing or attack attempts
- The attacker attempted to manipulate SQL query logic to bypass authentication controls

### Malicious Payload

```sql
' OR 1=1 --
```

This payload is commonly associated with SQL Injection attacks and is designed to alter application logic by forcing authentication conditions to evaluate as true.

---

## 🚨 Impact Assessment

- SQL Injection attempt confirmed
- Authentication bypass technique identified
- Repeated malicious requests observed
- No successful exploitation confirmed
- No evidence of unauthorized access identified

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| Payload | ' OR 1=1 -- |
| Technique | SQL Injection |
| Attack Method | Authentication Bypass |
| Target | Web Application Login Endpoint |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1190 | Exploit Public-Facing Application |

---

## 🛠️ Response Actions

- Classified alert as True Positive
- Investigated malicious requests
- Verified no successful compromise occurred
- Recommended continued monitoring of the affected application
- Recommended input validation and secure coding controls
- Recommended implementation of additional filtering and detection rules

---

## 📚 Conclusion

The investigation confirmed a SQL Injection attempt targeting a public-facing web application.

Analysis identified a known authentication bypass payload and multiple malicious requests consistent with SQL Injection activity. Although the attack was confirmed, no evidence indicated successful exploitation or unauthorized access.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Web Attack / SQL Injection Attempt**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Response**
