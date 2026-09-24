# 🪓 Brutus — Sherlock (Very Easy)

🔗 Completion Proof:  
[Hack The Box Achievement](https://labs.hackthebox.com/achievement/sherlock/2578759/631)

## 📝 Description

Brutus is a Sherlock challenge focused on **log forensics**, **incident investigation**, and identifying suspicious activity within a Linux environment.

The challenge simulated a system compromise through SSH brute-force attacks, requiring the analysis of system logs and forensic evidence to reconstruct the attack timeline.

## ✔ Skills Practiced

- Linux forensic log analysis (`auth.log` and `wtmp`)
- SSH authentication investigation
- Brute-force attack detection
- Analysis of suspicious IP addresses in access logs
- Extraction of login and logout information from audit files
- Incident timeline reconstruction
- Identification of successful authentication after repeated failed attempts
- Investigation of post-compromise activity
- Analysis of user creation and persistence-related events
- Evidence filtering and correlation using Linux commands

## 🛠 Tools Used

- Linux
- grep
- sort
- uniq
- last
- Manual log analysis
- Audit files (`auth.log` and `wtmp`)

## 🔎 Key Findings

During the investigation, authentication logs were analyzed to identify:

- Repeated SSH login attempts
- Origin of suspicious connections
- The point at which successful access was obtained
- Activities performed after the system compromise

The investigation was conducted by correlating multiple evidence sources, allowing the reconstruction of the attack sequence and the identification of attacker activity.

## 📚 Knowledge Gained

- Digital Forensics fundamentals
- Linux log analysis
- Security incident investigation
- Brute-force attack identification
- Basic Incident Response techniques
- Event correlation for attack reconstruction

---

# 🔍 HTB Sherlocks — Digital Forensics & Incident Investigation

Hack The Box Sherlocks are challenges focused on **digital forensics**, **log analysis**, **attack detection**, **malware analysis**, and **post-incident investigations**.

They simulate real-world security scenarios where analysts must collect evidence, understand the attack chain, and answer investigative questions using Blue Team, Threat Hunting, and Incident Response methodologies.
