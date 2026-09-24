# 🎣 PhishNet — Sherlock (Very Easy)

🔗 Completion Proof:  
[Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/985)

## 📝 Description

PhishNet is a beginner-friendly Sherlock focused on phishing email investigation and email forensics.

The challenge simulated the analysis of a suspicious email containing phishing indicators, malicious attachments, and social engineering techniques designed to trick the recipient into opening a harmful file.

The objective was to analyze the email structure, validate sender information, identify indicators of compromise, and determine the attack technique used during the campaign.

## ✔ Skills Practiced

- Email header analysis
- SMTP relay investigation
- Sender verification
- Reply-To analysis
- SPF validation
- Phishing domain identification
- Attachment analysis
- Base64 decoding
- SHA-256 hash calculation
- ZIP file inspection
- Malicious file identification
- MITRE ATT&CK mapping
- IOC extraction

## 🛠 Tools Used

- Linux
- grep
- Python
- Base64 decoding
- ExifTool
- Manual email analysis

## 🔎 Key Findings

During the investigation, it was possible to identify:

- Sender originating IP address
- Mail relay server involved in email delivery
- Sender and Reply-To email addresses
- SPF authentication result
- Phishing URL used in the campaign
- Fake company name used for social engineering
- Malicious ZIP attachment
- SHA-256 hash of the attachment
- Malicious payload hidden inside the ZIP archive

The attachment contained a disguised batch script using a double-extension filename technique to appear as a legitimate PDF document.

## 🧠 MITRE ATT&CK

- T1566.001 — Spearphishing Attachment
- T1204 — User Execution

## 📚 Knowledge Gained

- Email forensics fundamentals
- Phishing email analysis
- Header inspection techniques
- Attachment analysis workflows
- Threat indicator extraction
- Digital Forensics fundamentals
- Phishing detection methodologies
- MITRE ATT&CK classification

---

# 🔍 HTB Sherlocks — Digital Forensics & Incident Investigation

Hack The Box Sherlocks focus on:

- Digital Forensics
- Incident Response
- Log Analysis
- Malware Analysis
- Threat Hunting
- Evidence Collection
- IOC Analysis
- Security Investigations

These challenges simulate real-world scenarios where analysts must collect evidence, reconstruct attack timelines, identify attacker behavior, and validate threats using DFIR and Blue Team methodologies.
