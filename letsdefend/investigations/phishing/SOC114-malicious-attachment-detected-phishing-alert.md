# 🚨 SOC114 — Malicious Attachment Detected - Phishing Alert

## 🎯 Objective

Investigate a phishing alert involving a malicious email attachment, determine whether the attachment was delivered and opened, analyze the associated endpoint activity, and identify indicators of compromise.

---

## 📋 Alert Information

| Field             | Details                                                             |
| ----------------- | ------------------------------------------------------------------- |
| **Event ID**      | 45                                                                  |
| **Rule**          | SOC114 - Malicious Attachment Detected - Phishing Alert             |
| **Event Time**    | 2021-01-31 15:48:30 (+03:00)                                        |
| **Severity**      | High                                                                |
| **Alert Type**    | Exchange                                                            |
| **Role**          | Security Analyst                                                    |
| **Difficulty**    | Beginner                                                            |
| **Result**        | **True Positive**                                                   |
| **MITRE ATT&CK**  | T1598.001                                                           |
| **SMTP Address**  | 49.234.43.39                                                        |
| **Device Action** | Allowed                                                             |
| **Subject**       | Invoice                                                             |
| **Source**        | [accounting@cmail.carleton.ca](mailto:accounting@cmail.carleton.ca) |
| **Destination**   | [richard@letsdefend.io](mailto:richard@letsdefend.io)               |

---

## 📧 Email Analysis

The alert involved an email sent from:

**From:** `accounting@cmail.carleton.ca`
**To:** `richard@letsdefend.io`
**Subject:** `Invoice`

The email claimed that an invoice was attached to the message.

The attachment was identified as malicious and associated with **CVE-2017-11882**, a vulnerability affecting Microsoft Office Equation Editor.

### Evidence

<img width="1439" height="716" alt="image" src="https://github.com/user-attachments/assets/601dd2eb-939c-4178-9194-6cebbea8cecd" />

---

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/a9f57907-2ecd-4f47-93ba-194e0b16c276" />

---

<img width="1439" height="816" alt="image" src="https://github.com/user-attachments/assets/b7c5bff3-b532-4ce2-bb82-76de2d9f69cc" />


---

## 🦠 Attachment Analysis

VirusTotal analysis identified the attachment as malicious.

* **Detection:** 36/62 security vendors
* **SHA-256:** `44e65a641fb970031c5efed324676b5018803e0a768608d3e186152102615795`
* **File type:** XLSX
* **Size:** 2.12 MB
* **Tags:** `exploit`, `executes-dropped-file`, `cve-2017-11882`
* **Categories:** Trojan, Phishing, Downloader

The results indicate that the attachment was associated with exploit and malware-delivery activity.

---

## 💻 Endpoint Investigation

The affected endpoint was:

| Field                | Details          |
| -------------------- | ---------------- |
| **Hostname**         | RichardPRD       |
| **IP Address**       | 172.16.17.45     |
| **User**             | richard          |
| **Operating System** | Windows 10       |
| **Domain**           | letsdefend.local |

The following legitimate processes were observed:

* `EXCEL.EXE`
* `OUTLOOK.EXE`
* `notepad.exe`
* `EQNEDT32.EXE`
* `ccsvchst.exe`

No malicious detections were identified for these processes.

### Malicious Process

A suspicious executable was identified at:

`C:\User\Public\JuicyPotato.exe`

The process was running as:

`NT AUTHORITY\SYSTEM`

This indicates execution with elevated system privileges.

![JuicyPotato running as NT AUTHORITY\SYSTEM](evidence/SOC114/juicy-potato-system.png)

---

## 🔍 JuicyPotato Analysis

VirusTotal analysis confirmed the executable as malicious:

* **File:** `JuicyPotato.exe`
* **Detection:** **57/69 security vendors**
* **SHA-256:** `0f56c703e9b7ddeb90646927bac05a5c6d95308c8e13b88e5d4f4b572423e036`
* **Categories:** HackTool, Trojan, PUA
* **Threat family:** JuicyPotato / JPotato
* **Community score:** -178

The high detection rate across multiple security vendors provides strong evidence that the executable is malicious.

![JuicyPotato VirusTotal analysis](evidence/SOC114/juicy-potato-virustotal.png)

---

## 🌐 Network Activity

Additional external network connections were observed from the affected endpoint.

These connections were treated as indicators requiring further investigation. The available evidence does not establish the exact purpose or command-and-control relationship of each connection.

---

## 🧠 Investigation Findings

| Finding                      | Result |
| ---------------------------- | ------ |
| Email delivered to user      | ✅ Yes  |
| Malicious attachment present | ✅ Yes  |
| Attachment opened            | ✅ Yes  |
| Attachment malicious         | ✅ Yes  |
| CVE-2017-11882 associated    | ✅ Yes  |
| Malicious process identified | ✅ Yes  |
| `JuicyPotato.exe` detected   | ✅ Yes  |
| Process executed as SYSTEM   | ✅ Yes  |
| Endpoint compromise evidence | ✅ Yes  |

The evidence confirms that the phishing email contained a malicious attachment and that malicious activity was subsequently identified on the affected endpoint.

The presence of `JuicyPotato.exe` running under `NT AUTHORITY\SYSTEM` provides evidence of malicious execution with elevated privileges.

The available evidence does **not** conclusively establish that the phishing attachment directly dropped or executed `JuicyPotato.exe`; therefore, the exact process/file lineage should not be assumed.

---

## 🎯 MITRE ATT&CK

**T1598.001 — Phishing for Information: Spearphishing Service**

The alert is mapped by LetsDefend to MITRE ATT&CK technique `T1598.001`.

---

## 📝 Conclusion

The investigation confirmed a **True Positive**.

The email was delivered to the user and contained a malicious attachment associated with CVE-2017-11882. Endpoint investigation also identified `JuicyPotato.exe`, which was confirmed malicious by VirusTotal and was executed under `NT AUTHORITY\SYSTEM`.

The combination of a malicious phishing attachment and confirmed malicious endpoint activity indicates that the alert represents a genuine security incident within the LetsDefend training environment.

---

## 🛠️ Skills Demonstrated

* Phishing Email Analysis
* Malicious Attachment Analysis
* VirusTotal Analysis
* Endpoint Investigation
* Process Analysis
* Malware Identification
* IOC Analysis
* Privilege Analysis
* MITRE ATT&CK Mapping
* SOC Alert Triage
* Incident Classification
* Security Investigation Reporting
