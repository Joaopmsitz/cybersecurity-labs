# RDP Brute Force Detected

## 1. Alert Summary

| Field | Value |
|---|---|
| LetsDefend Event ID | 234 |
| Detection Rule | SOC176 - RDP Brute Force Detected |
| Category | Brute Force |
| Affected Asset / User | Matthew |
| Target IP | `172.16.17.148` |
| Source IP | `218.92.0.56` |
| Target Service | Remote Desktop Protocol (RDP) |
| Destination Port | TCP/3389 |
| Connection Attempts | 15 |
| Authentication Evidence | Windows Security Event IDs 4625 and 4624 (Logon Type 10) |
| Investigation Verdict | True Positive |
| Containment | Endpoint recorded as contained in the analyst notes |

## 2. Investigation Overview

The alert was generated after repeated RDP connection attempts targeted Matthew's endpoint at `172.16.17.148` from the external source `218.92.0.56`.

Firewall telemetry recorded 15 connection attempts to TCP port 3389. Windows Security logs showed multiple failed logons (Event ID 4625), followed by a successful RemoteInteractive logon (Event ID 4624, Logon Type 10).

After the successful authentication, command activity indicated account, group, and network-connection discovery. The combination of repeated authentication failures, a subsequent successful RDP session, and post-authentication reconnaissance supports a True Positive classification.

## 3. Evidence Analysis

### RDP Connection Attempts

| Attribute | Evidence |
|---|---|
| Source IP | `218.92.0.56` |
| Target IP | `172.16.17.148` |
| Protocol | RDP over TCP |
| Destination Port | `3389` |
| Attempts | 15 |

The repeated connections to the RDP service indicate password-guessing activity against the target endpoint.

### Windows Authentication Logs

The authentication sequence included:

- **Event ID 4625:** multiple failed logon attempts.
- **Event ID 4624, Logon Type 10:** a successful RemoteInteractive logon.

These are Windows Security Event IDs, not LetsDefend alert IDs. The successful Logon Type 10 event establishes that an RDP authentication succeeded after the recorded failures.

### Post-Authentication Activity

The investigation recorded the following commands:

```text
whoami
net user letsdefend
net localgroup administrators
netstat -ano
```

The commands are consistent with post-authentication reconnaissance:

- `whoami` identifies the current security context.
- `net user letsdefend` queries information about the specified local account.
- `net localgroup administrators` lists membership of the local Administrators group; the command alone does not prove that a user was added to that group.
- `netstat -ano` displays network connections and associated process IDs.

The available command history supports discovery activity. It does not, by itself, establish account creation, privilege modification, persistence, or data exfiltration.

### Additional Enrichment

The IP address `118.69.65.60` appeared in playbook enrichment, but the available investigation records did not correlate it with the observed RDP session. It is therefore not treated as a confirmed source indicator for this incident.

### Endpoint Status

The original analyst notes record that the affected endpoint was contained. The available evidence does not establish additional remediation details or the exact time containment was completed.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Repeated RDP authentication attempts, including 15 recorded connections and multiple failed logons |
| [T1021.001](https://attack.mitre.org/techniques/T1021/001/) | Remote Services: Remote Desktop Protocol | Successful RemoteInteractive logon (Windows Event ID 4624, Logon Type 10) |
| [T1033](https://attack.mitre.org/techniques/T1033/) | System Owner/User Discovery | `whoami` command |
| [T1087.001](https://attack.mitre.org/techniques/T1087/001/) | Account Discovery: Local Account | `net user letsdefend` command |
| [T1069.001](https://attack.mitre.org/techniques/T1069/001/) | Permission Groups Discovery: Local Groups | `net localgroup administrators` command |
| [T1049](https://attack.mitre.org/techniques/T1049/) | System Network Connections Discovery | `netstat -ano` command |

T1078.002 (Domain Accounts) is not mapped because the available evidence does not establish that the authenticated account was a domain account.

## 5. Response Actions

### Investigation Performed

- Reviewed the RDP alert and firewall connection records.
- Correlated the 15 connection attempts with Windows Security authentication events.
- Identified the successful RemoteInteractive logon following multiple failures.
- Reviewed post-authentication command activity.
- Distinguished confirmed source activity from an uncorrelated enrichment IP.
- Recorded the endpoint containment status from the original analyst notes.

### Recommended Follow-up

- Verify that the affected account's password was reset and that MFA is enforced where supported.
- Review other endpoints for authentication attempts from `218.92.0.56`.
- Inspect the successful session for additional process, file, and network activity.
- Confirm that containment and account-remediation actions were completed and documented.

These follow-up items are recommendations; they are not represented as completed actions in this report.

## 6. Conclusion

The investigation confirmed a **True Positive RDP brute-force incident** targeting `172.16.17.148`. Fifteen connection attempts from `218.92.0.56` were recorded, followed by a successful RDP authentication (Windows Event ID 4624, Logon Type 10) after multiple failures.

Commands executed after authentication showed account, local-group, and network-connection discovery. The analyst notes record that the affected endpoint was contained. The available evidence does not establish that an account was modified, that persistence was created, or that data was exfiltrated.

**Final Verdict: True Positive**

**Impact Assessment: Successful RDP Authentication Followed by Reconnaissance - Endpoint Containment Recorded**
