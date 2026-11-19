# Brute Force Investigations

Documented investigations involving authentication attacks, password guessing, and unauthorized remote access.

## Investigations

| Event ID | Detection Rule | Investigation Focus | Verdict |
|---:|---|---|---|
| 234 | SOC176 | RDP brute force, successful authentication, and post-authentication reconnaissance | True Positive |

[View EventID 234 - RDP Brute Force Detected](./eventid234-rdp-brute-force-detected.md)

## Investigation Highlights

### EventID 234 - RDP Brute Force Detected

The investigation identified repeated RDP connection attempts from 218.92.0.56 against Matthew (172.16.17.148).

Firewall logs recorded 15 connection attempts targeting TCP port 3389. Windows Security logs showed multiple failed logons (Event ID 4625), followed by a successful RemoteInteractive logon (Event ID 4624, Logon Type 10).

Post-authentication commands included:

- whoami
- net user letsdefend
- net localgroup administrators
- netstat -ano

The original Analyst Note records that the affected endpoint was contained.

## Topics Covered

- RDP brute-force investigation
- Firewall traffic and source IP analysis
- Windows Security Event ID 4625 and 4624
- Successful remote authentication
- Post-authentication reconnaissance
- Account and group enumeration
- Network connection discovery
- Endpoint containment

## Scope

This directory contains simulated LetsDefend training investigations. Findings and response actions should not be interpreted as real-world incident response experience.

[Back to Investigation Catalog](../README.md) · [Back to LetsDefend](../../README.md)
