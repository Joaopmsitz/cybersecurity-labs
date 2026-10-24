# Let'sDefend — SOC Investigations

This section documents investigation practice completed on the Let'sDefend platform. The focus is alert triage, evidence review, threat validation, indicator analysis, and defensible incident decisions.

- Platform profile: [JoaoPmsItz](https://app.letsdefend.io/user/JoaoPmsItz)
- GitHub profile: [Joaopmsitz](https://github.com/Joaopmsitz)

## Skills practiced

- SOC alert triage and investigation.
- Phishing and suspicious-attachment analysis.
- Malware and script-related alerts.
- Web attack indicators.
- IOC identification and threat-intelligence validation.
- Network and process analysis.
- MITRE ATT&CK mapping when supported by the evidence.
- Incident response documentation and final disposition.

## Investigation categories

| Category | Examples currently listed in this portfolio |
|---|---|
| [Malware](./investigations/malware/) | SOC104 — Malware Detected; SOC137 — Malicious File/Script Download Attempt; SOC138 — Suspicious XLS File Detection; SOC205 — Malicious Macro Execution |
| [Phishing](./investigations/phishing/) | SOC140 — Phishing Malicious Attachment; SOC141 — Phishing URL Detected; SOC146 — Excel 4.0 Macro-related phishing; SOC282 — Phishing Deceptive Email; SOC338 — Lumma Stealer ClickFix Phishing |
| [Web attacks](./investigations/web-attacks/) | SOC165 — Possible SQL Injection Payload Detected; SOC166 — JavaScript Code Detected in URL |
| [Brute force](./investigations/brute-force/) | SOC176 — RDP Brute Force Detection |

The case names above are an index of topics represented in the current README. Link each case ID to its individual write-up once the corresponding file path has been verified; do not leave a case listed as a completed write-up if only the training alert was completed and no documentation was published.

## Investigation workflow

1. **Detection:** review the alert, source, time window, and available context.
2. **Triage:** validate whether the activity is expected, suspicious, or clearly malicious.
3. **Evidence review:** inspect relevant logs, processes, URLs, files, network indicators, or related events.
4. **Correlation:** compare evidence with known context and threat intelligence where appropriate.
5. **Disposition:** document the conclusion, confidence, and rationale.
6. **Response:** record any response recommendation or action actually taken; do not claim containment if none occurred.
7. **Lessons learned:** note detection gaps, limitations, and follow-up ideas.

## Write-up quality checklist

A strong investigation should include the alert objective, relevant evidence, analysis, IOCs when available, ATT&CK mapping only when justified, final verdict, response rationale, and sanitized screenshots. Clearly label simulated exercise data and avoid publishing credentials, personal information, or restricted platform content.

[Back to the main portfolio](../README.md)
