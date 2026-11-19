# Brute Force Investigations

Documented SOC investigations focused on authentication attacks, brute-force activity, unauthorized remote access, and post-authentication behavior.

## Investigations

| Event ID | Detection Rule | Investigation Focus | Verdict |
|---:|---|---|---|
| 234 | SOC176 | RDP brute force, successful authentication, and post-authentication reconnaissance | True Positive |

[View EventID 234 - RDP Brute Force Detected](./eventid234-rdp-brute-force-detected.md)

## Investigation Highlights

### EventID 234 - RDP Brute Force Detected

The investigation identified repeated RDP connection attempts originating from `218.92.0.56` against the host `Matthew` (`172.16.17.148`).

Firewall logs recorded 15 connection attempts targeting TCP port 3389. Windows Security logs showed multiple failed logons (Event ID 4625), followed by a successful authentication (Event ID 4624) using the `Matthew` account.

Post-authentication activity included reconnaissance commands:

- `whoami`
- `net user`
- `net localgroup administrators`
- `netstat -ano`

The analyst note records that the affected host was contained.

### Investigation Outcome

**True Positive — Successful RDP access followed by post-authentication reconnaissance.**

## Topics Covered

- RDP brute-force investigation
- Firewall traffic and source IP analysis
- Windows Security Event ID 4625 - Failed Logon
- Windows Security Event ID 4624 - Successful Logon
- Successful remote authentication
- Post-authentication reconnaissance
- Windows account and network enumeration
- Threat intelligence and IP reputation
- Host containment and incident response
- MITRE ATT&CK mapping

## MITRE ATT&CK

| Technique | Technique Name |
|---|---|
| T1110 | Brute Force |
| T1078 | Valid Accounts |
| T1078.002 | Domain Accounts |
| T1087 | Account Discovery |
| T1059 | Command and Scripting Interpreter |
| T1059.003 | Windows Command Shell |

These mappings reflect the techniques recorded in the original investigation. Their applicability should be evaluated against the supporting evidence in the individual report.

## Scope

This directory contains simulated LetsDefend training investigations. Findings and response actions refer to the documented scenarios and should not be interpreted as real-world incident response experience.

---

[Back to Investigation Catalog](../README.md) · [Back to LetsDefend](../../README.md)
