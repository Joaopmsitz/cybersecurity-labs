# LetsDefend — Investigation Catalog

Central index of SOC investigation reports completed in the LetsDefend training environment.

This directory organizes individual case analyses by security alert category.

## Documented Investigation Inventory

| Category | Reports | Case IDs | Investigation Focus |
|---|---:|---|---|
| [Brute Force](./brute-force/README.md) | 1 | SOC176 | RDP authentication attacks and brute-force detection. |
| [Malware](./malware/README.md) | 5 | SOC104, SOC106, SOC137, SOC138, SOC205 | Suspicious files, malware detection, script downloads, and malicious macros. |
| [Phishing](./phishing/README.md) | 7 | SOC114, SOC120, SOC140, SOC141, SOC146, SOC282, SOC338 | Phishing emails, suspicious URLs, and malicious attachments. |
| [Web Attacks](./web-attacks/README.md) | 2 | SOC165, SOC166 | SQL injection indicators and suspicious JavaScript in URLs. |

**Total: 15 documented investigation reports.**

## Platform Activity vs. Repository Documentation

The [public LetsDefend profile](https://app.letsdefend.io/user/JoaopmsItz) displays platform-wide performance metrics, including a 94% success rate and activity across multiple alert categories.

These metrics describe platform activity and are not equivalent to the number of individual reports published here.

- **Platform activity:** Alert-category values and performance metrics displayed by LetsDefend.
- **Repository documentation:** 15 individual investigation reports currently organized in this directory.

Not every investigated alert necessarily has a dedicated GitHub report.

## Investigation Methodology

The reports follow an evidence-based investigation approach:

1. **Alert Triage** — Review alert metadata, severity, affected assets, and detection context.
2. **Evidence Collection** — Examine available logs, endpoint telemetry, processes, network activity, and artifacts.
3. **Threat Validation** — Correlate indicators with threat intelligence and external security analysis.
4. **Technical Analysis** — Evaluate suspicious behavior and distinguish observed evidence from assumptions.
5. **Response Assessment** — Review containment actions and incident response procedures.
6. **Classification** — Document the final assessment and supporting evidence.

## Documentation Principles

- Conclusions should be supported by available evidence.
- Missing telemetry should not automatically be interpreted as proof that an activity did not occur.
- Antivirus and threat intelligence results must be evaluated in context.
- MITRE ATT&CK mappings should reflect observed or sufficiently supported behavior.
- Platform results and analyst conclusions should be documented separately when discrepancies occur.

## Scope

These are controlled LetsDefend training exercises. Findings and response actions refer to simulated scenarios and should not be interpreted as real-world incident response engagements.

---

[Back to LetsDefend](../README.md) · [Back to Cybersecurity Portfolio](../../README.md)
