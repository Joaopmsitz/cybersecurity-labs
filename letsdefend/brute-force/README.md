# Brute Force Investigations

Documented investigations involving attempts to gain unauthorized access by guessing or spraying credentials against network services and remote-access interfaces.

## Investigations

| Event ID | Detection Rule | Investigation Report | Verdict |
|---:|---|---|---|
| 234 | SOC176 | [RDP Brute Force Detected](./eventid234-rdp-brute-force-detected.md) | True Positive |

## Topics Covered

- Brute-force and password-spraying patterns
- Failed and successful authentication analysis
- Network services and remote-access protocols, including RDP, SSH, and VPN
- Source IP and destination service analysis
- Windows and Linux authentication logs
- Account and permission-group discovery after authentication
- Correlation of network and endpoint telemetry
- Account protection, containment, and remediation assessment

## Scope

These reports document simulated LetsDefend training scenarios. Findings and response actions should not be interpreted as real-world incident response engagements.

---

[Back to Investigation Catalog](../README.md) · [Back to LetsDefend](../../README.md)
