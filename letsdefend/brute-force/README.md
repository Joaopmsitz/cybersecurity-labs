# Brute Force Investigations

Documented investigations involving authentication attacks, password guessing, and unauthorized remote access.

## Investigations

| Event ID | Detection Rule | Investigation Focus | Verdict |
|---:|---|---|---|
| 234 | SOC176 | RDP brute force, successful authentication, and post-authentication reconnaissance | True Positive |

## Investigation Highlights

### EventID 234 - RDP Brute Force Detected

Fifteen RDP connection attempts from `218.92.0.56` targeted Matthew's endpoint (`172.16.17.148`). Windows Security logs recorded multiple failed logons (Event ID 4625), followed by a successful RemoteInteractive logon (Event ID 4624, Logon Type 10).

Post-authentication commands included `whoami`, `net user letsdefend`, `net localgroup administrators`, and `netstat -ano`, indicating user, account, group, and network-connection discovery. The analyst notes record that the affected endpoint was contained.

[Read the full EventID 234 investigation](./eventid234-rdp-brute-force-detected.md).

## Topics Covered

- RDP brute-force investigation
- Firewall traffic and source IP analysis
- Windows Security Event IDs 4625 and 4624
- Successful remote authentication (Logon Type 10)
- Post-authentication reconnaissance
- Account and local-group discovery
- Network connection discovery
- Endpoint containment assessment

## Scope

This directory contains simulated LetsDefend training investigations. Findings and response actions should not be interpreted as real-world incident response engagements.

---

[Back to Investigation Catalog](../README.md) Â· [Back to Cybersecurity Labs](../../README.md)
