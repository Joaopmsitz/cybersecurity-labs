# 🚨 SOC176 - RDP Brute Force Detected

## 📌 Summary

An RDP brute force attack was detected against the host **Matthew (172.16.17.148)**.

The investigation revealed multiple failed authentication attempts originating from a single external IP address, followed by a successful Remote Desktop logon and post-compromise reconnaissance activity.

---

## 🧾 Alert Details

| Field | Value |
|---------|---------|
| Alert ID | SOC176 |
| Event ID | 234 |
| Category | Brute Force |
| Source IP | 218.92.0.56 |
| Destination IP | 172.16.17.148 |
| Destination Host | Matthew |
| Protocol | RDP |
| Firewall Action | Allowed |

---

## 🔍 Investigation

### Key Findings

- Multiple failed RDP authentication attempts detected
- Event ID 4625 observed for failed logons
- Successful Event ID 4624 authentication identified
- Successful RemoteInteractive (Logon Type 10) session established
- Attacker performed post-authentication reconnaissance
- Endpoint was successfully contained

### Failed Authentication

```text
Event ID: 4625
Username: admin
Error Code: 0xC000006D
Source IP: 218.92.0.56
```

### Successful Authentication

```text
Event ID: 4624
Username: Matthew
Logon Type: 10 (RemoteInteractive)
Source IP: 218.92.0.56
```

### Observed Commands

```cmd
whoami
net user letsdefend
net localgroup administrators
netstat -ano
```

These commands indicate account discovery, privilege enumeration, and network reconnaissance activities following successful access.

---

## 🔗 Indicators of Compromise (IOCs)

| Type | Indicator |
|---------|---------|
| Source IP | 218.92.0.56 |
| Target Host | Matthew |
| Target IP | 172.16.17.148 |
| Protocol | RDP (3389) |

---

## 🧠 MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1110 | Brute Force |
| T1021.001 | Remote Services: RDP |
| T1087 | Account Discovery |
| T1069 | Permission Group Discovery |
| T1016 | System Network Configuration Discovery |

---

## 🛠️ Response Actions

- Validated malicious source IP activity
- Confirmed brute force attack attempts
- Identified successful RDP authentication
- Reviewed post-compromise commands
- Contained the affected endpoint
- Classified alert as True Positive

---

## 📚 Conclusion

The investigation confirmed a successful RDP brute force attack originating from **218.92.0.56** against the host **Matthew**.

After multiple failed authentication attempts, the attacker successfully logged in via RDP and executed reconnaissance commands to gather information about users, privileges, and network connections.

The compromised endpoint was isolated to prevent further attacker activity.

## ✅ Final Verdict

**True Positive**

## 🎯 Classification

**Brute Force / Unauthorized RDP Access / Post-Compromise Reconnaissance**

---

⭐ SOC investigation completed following the workflow:

**Detection → Analysis → Threat Validation → Containment**
