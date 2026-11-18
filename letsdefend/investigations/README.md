# LetsDefend — Investigation Catalog

Central index of documented SOC investigations completed on LetsDefend.

The cases are organized by attack category. Each category contains an index of its investigations and individual reports documenting the evidence, analysis, and conclusions.

## Investigation Inventory

| Category | Cases | Case IDs | Investigation Focus |
|---|---:|---|---|
| [Brute Force](./brute-force/README.md) | 1 | SOC176 | RDP authentication attacks and brute-force detection. |
| [Malware](./malware/README.md) | 5 | SOC104, SOC106, SOC137, SOC138, SOC205 | Suspicious files, malware detection, script downloads, and malicious macros. |
| [Phishing](./phishing/README.md) | 7 | SOC114, SOC120, SOC140, SOC141, SOC146, SOC282, SOC338 | Phishing emails, malicious attachments, suspicious URLs, and delivery techniques. |
| [Web Attacks](./web-attacks/README.md) | 2 | SOC165, SOC166 | SQL injection indicators and suspicious JavaScript in HTTP requests. |

**Total: 15 documented investigations.**

## Investigation Methodology

The reports follow an evidence-based investigation approach:

1. **Alert Triage** — Review alert metadata, severity, affected assets, and detection context.
2. **Evidence Collection** — Examine relevant logs, endpoint telemetry, processes, network activity, and other available artifacts.
3. **Threat Validation** — Correlate indicators with threat intelligence and external security analysis when appropriate.
4. **Technical Analysis** — Evaluate suspicious behavior, identify relevant attack techniques, and distinguish observed evidence from assumptions.
5. **Response Assessment** — Review containment actions and the expected incident response playbook.
6. **Classification** — Document the final assessment and its supporting evidence.

## Documentation Principles

- Conclusions must be supported by the available evidence.
- Missing telemetry must not automatically be interpreted as proof that an activity did not occur.
- Threat intelligence and antivirus results must be evaluated in context.
- MITRE ATT&CK mappings should reflect observed or sufficiently supported behavior.
- Platform results and analyst conclusions should be documented separately when discrepancies occur.

## Scope

These are controlled training exercises completed on LetsDefend. The reports demonstrate investigation methodology and technical learning rather than real-world incident response engagements.

---

[Back to LetsDefend](../README.md) · [Back to Cybersecurity Portfolio](../../README.md)
