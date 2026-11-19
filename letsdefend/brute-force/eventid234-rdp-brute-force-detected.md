# RDP Brute Force Detected

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 234 |
| Detection Rule | SOC176 - RDP Brute Force Detected |
| Event Time | 2024-03-07 11:44:00 (UTC+03:00) |
| Severity | Medium |
| Category | Brute Force |
| Source IP | `218.92.0.56` |
| Destination Host | Matthew |
| Destination IP | `172.16.17.148` |
| Protocol | RDP |
| Destination Port | 3389 |
| Firewall Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

The investigation identified repeated RDP authentication attempts originating from `218.92.0.56` against the host Matthew (`172.16.17.148`).

Analysis revealed 15 firewall log entries targeting TCP port 3389, followed by a successful Remote Desktop authentication after multiple failed logon attempts.

Post-authentication activity included account, privilege group, and network connection enumeration. The original Analyst Note records that the affected endpoint was contained.

### Key Findings

- Multiple failed authentication attempts from a single external IP.
- Windows Security Event ID 4625 recorded failed logons.
- Windows Security Event ID 4624 confirmed successful authentication.
- Logon Type 10 indicated an interactive RDP session.
- Post-authentication reconnaissance commands were executed.
- The Analyst Note records successful endpoint containment.

## 3. Evidence Analysis

### Network Activity

Firewall logs identified 15 connection attempts from `218.92.0.56` targeting Matthew (`172.16.17.148`) over TCP port 3389.

The original threat intelligence enrichment also identified the source IP as suspicious, with 11 antivirus engines flagging it on VirusTotal.

### Authentication Events

**Failed Authentication**

```text
Windows Event ID: 4625
Username: admin
Status / Error Code: 0xC000006D
Source IP: 218.92.0.56
```

**Successful Authentication**

```text
Windows Event ID: 4624
Username: Matthew
Logon Type: 10 (RemoteInteractive)
Source IP: 218.92.0.56
```

The successful logon following repeated failures indicates unauthorized RDP access to the target host.

### Post-Authentication Activity

The Analyst Note documented the following commands:

```cmd
whoami
net user letsdefend
net localgroup administrators
netstat -ano
```

These commands indicate reconnaissance activity:

- `whoami`: identifies the current user context.
- `net user letsdefend`: queries local account information.
- `net localgroup administrators`: enumerates local administrator group membership.
- `netstat -ano`: displays network connections and associated process IDs.

### Indicator Review

| Type | Indicator | Assessment |
|---|---|---|
| Source IP | `218.92.0.56` | Suspicious external source |
| Destination Host | Matthew | Affected endpoint |
| Destination IP | `172.16.17.148` | Target system |
| Protocol | RDP | Remote access service |
| Destination Port | 3389/TCP | RDP |

A separate playbook enrichment entry also mentions `118.69.65.60`. The available records do not establish that this address is associated with the 15 firewall connections attributed to `218.92.0.56`; the two indicators should not be conflated.

### External Reference

[Independent EventID 234 investigation](https://medium.com/@edukayky/soc-alert-rdp-brute-force-detected-by-letsdefend-50da65a89711)

This source is included for contextual comparison, not as evidence collected during this investigation.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1110 | Brute Force | Repeated failed authentication attempts |
| T1021.001 | Remote Desktop Protocol | Successful RDP authentication |
| T1087.001 | Account Discovery: Local Account | `net user letsdefend` |
| T1069.001 | Permission Groups Discovery: Local Groups | `net localgroup administrators` |
| T1049 | System Network Connections Discovery | `netstat -ano` |

The mappings are based on the authentication and post-authentication activity documented in the investigation.

## 5. Response Actions

### Investigation Performed

- Reviewed firewall logs and identified repeated RDP connection attempts.
- Correlated failed and successful Windows authentication events.
- Confirmed the successful RemoteInteractive logon.
- Examined post-authentication reconnaissance commands.
- Reviewed source IP reputation using threat intelligence.
- Classified the alert as True Positive.

### Containment

The original Analyst Note records that the affected endpoint was contained to prevent further unauthorized access.

## 6. Conclusion

The investigation confirmed a successful RDP brute-force incident originating from `218.92.0.56` against Matthew (`172.16.17.148`).

Multiple failed authentication attempts were followed by a successful RDP session using the Matthew account. Subsequent commands demonstrated account, privilege group, and network connection discovery.

The original investigation record states that the affected endpoint was contained.

**Final Verdict: True Positive**

**Incident Classification: RDP Brute Force, Unauthorized Remote Access and Post-Authentication Discovery**
