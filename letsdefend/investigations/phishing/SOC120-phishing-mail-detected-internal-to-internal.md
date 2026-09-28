# 🎣 SOC120 — Phishing Mail Detected - Internal to Internal

## 📌 Alert Overview

| Field                   | Value                                                  |
| ----------------------- | ------------------------------------------------------ |
| **Event ID**            | 52                                                     |
| **Rule**                | SOC120 - Phishing Mail Detected - Internal to Internal |
| **Alert Type**          | Exchange                                               |
| **Role**                | Security Analyst                                       |
| **Difficulty**          | Beginner                                               |
| **Device Action**       | Allowed                                                |
| **Email Subject**       | Meeting                                                |
| **Source Address**      | [john@letsdefend.io](mailto:john@letsdefend.io)        |
| **Destination Address** | [susie@letsdefend.io](mailto:susie@letsdefend.io)      |
| **Disposition**         | False Positive                                         |

---

## 🎯 Objective

Investigate an email flagged by the SOC120 phishing detection rule and determine whether the message represents a genuine phishing attempt or legitimate internal communication.

---

## 📧 Email Analysis

### Message Details

| Field         | Value                                             |
| ------------- | ------------------------------------------------- |
| **From**      | [john@letsdefend.io](mailto:john@letsdefend.io)   |
| **To**        | [susie@letsdefend.io](mailto:susie@letsdefend.io) |
| **Subject**   | Meeting                                           |
| **Sender IP** | 172.16.20.3                                       |
| **Date**      | 2021-02-06 22:24:09 BRT                           |
| **Action**    | Unknown                                           |

### Email Content

> Hi Susie, Can we arrange a meeting today if you are available?

The message is a short internal communication regarding a meeting.

No malicious URL, attachment, credential request, or suspicious instruction was identified in the email content provided.

### Evidence

<img width="1439" height="697" alt="image" src="https://github.com/user-attachments/assets/81f17250-775c-487b-870c-d6db7006dd06" />

---

## 🌐 Network Evidence

The email transaction was observed between JohnComputer and the internal Exchange/SMTP server:

```text
2021-02-06 22:23:51
Exchange
Source: 172.16.17.82:49582
Destination: 172.16.20.3:25
```

### Communication Flow

```text
JohnComputer
172.16.17.82
      │
      │ SMTP
      │ TCP/25
      ▼
Exchange Server
172.16.20.3
      │
      ▼
john@letsdefend.io
      │
      │ Internal Email
      ▼
susie@letsdefend.io
```

---

## 🖥️ Endpoint Investigation

### Host Information

| Field                | Value               |
| -------------------- | ------------------- |
| **Hostname**         | JohnComputer        |
| **Domain**           | LetsDefend          |
| **IP Address**       | 172.16.17.82        |
| **Operating System** | Windows 10          |
| **Bit Level**        | 64-bit              |
| **Primary User**     | John                |
| **Client/Server**    | Client              |
| **Last Login**       | 2020-10-10 12:53:37 |

### Browser History

Observed activity included:

* Google Chrome support page
* Google search for updating Chrome
* LetsDefend GitHub repository

No suspicious phishing domain or malicious URL was identified in the provided browser history.

### Command History

Observed commands:

```text
net user
users
dir /s
dir
ping raw.githubusercontent.com
```

These commands alone do not provide sufficient evidence of compromise or malicious activity.

---

## 🔎 Investigation Findings

The investigation identified the following:

* The sender and recipient belong to the same internal domain.
* The email contains a simple meeting request.
* No malicious attachment was identified.
* No suspicious URL was identified.
* No credential-harvesting request was identified.
* The endpoint history did not reveal clear indicators of compromise.
* The observed SMTP communication was directed to the internal Exchange server.
* No evidence was identified linking the email to malware delivery or successful phishing activity.

---

## 🧠 Analysis

Although the email triggered the **SOC120 - Phishing Mail Detected - Internal to Internal** rule, the available evidence does not support classification as a malicious phishing message.

The alert appears to have been triggered by the characteristics of the email communication rather than by confirmed malicious content or endpoint compromise.

---

## ✅ Conclusion

**Disposition: False Positive**

No evidence of compromise or malicious activity was identified during the investigation.

The email was an internal communication between `john@letsdefend.io` and `susie@letsdefend.io` concerning a meeting, with no malicious links, attachments, credential requests, or other suspicious content identified.

**Recommended Action:** Close the alert as a false positive. No containment or remediation action is required based on the available evidence.

---

## 🛠️ SOC Skills Demonstrated

* Alert Triage
* Email Analysis
* SMTP Traffic Analysis
* Endpoint Investigation
* Browser History Analysis
* Command-Line Investigation
* False Positive Identification
* Threat Classification
* Incident Documentation
