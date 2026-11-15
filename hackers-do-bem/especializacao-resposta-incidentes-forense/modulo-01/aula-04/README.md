# Hackers do Bem — Specialization | Module 01 — Class 04

This class explores Network Security Monitoring (NSM), Enterprise Security Monitoring (ESM), data decoding, detection engineering, incident response playbooks, and threat behavior analysis. The practical activities combine CyberChef, Sigma, ElastAlert, and MITRE ATT&CK Navigator.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Specialization |
| Module | 01 |
| Class | 04 |
| Activities | 5 |
| Main Topics | Network Security Monitoring, CyberChef, Cryptographic Decoding, Incident Response Playbooks, Sigma Rules, ElastAlert, and MITRE ATT&CK |

## Practical Activities

| Activity | Topic | Description | Documentation |
| -------- | ----- | ----------- | ------------- |
| 4.1 — Getting Started with CyberChef | Data Decoding | Decode a hexadecimal string protected with a single-byte XOR key using brute-force analysis. | [View Activity](./atividade-4.1-cyberchef-xor-brute-force/README.md) |
| 4.2 — Solving Simple Cryptography Challenges with CyberChef | Cryptographic Decoding | Automate Morse code normalization and decoding using sequential CyberChef operations. | [View Activity](./atividade-4.2-cyberchef-morse-decoding/README.md) |
| 4.3 — Incident Response Playbook: Malware on a Server | Incident Response | Develop a server malware incident response playbook covering preparation, identification, containment, eradication, and recovery. | [View Activity](./atividade-4.3-malware-incident-response-playbook/README.md) |
| 4.4 — Converting Playbooks for Incident Response Platforms | Detection Engineering | Create a Sigma rule for chattr immutable attribute removal and convert it to ElastAlert. | [View Activity](./atividade-4.4-sigma-to-elastalert/README.md) |
| 4.5 — MITRE ATT&CK Navigator: APT3 and APT29 | Threat Intelligence | Compare APT3 and APT29 techniques using scored and combined MITRE ATT&CK Navigator layers. | [View Activity](./atividade-4.5-mitre-attack-navigator-apt3-apt29/README.md) |

## Environment

The activities primarily use browser-based security tools and online analysis platforms.

| Component | Tool |
|---|---|
| Data Decoding | CyberChef |
| Detection Rule Format | Sigma |
| Rule Conversion | Uncoder IO |
| Alerting Format | ElastAlert |
| Threat Behavior Analysis | MITRE ATT&CK Navigator |
| Threat Emulation Reference | Atomic Red Team |

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Data Analysis | CyberChef | Decode, transform, and manipulate encoded data. |
| Detection Engineering | Sigma | Describe security detections in a generic, vendor-independent format. |
| Rule Conversion | Uncoder IO | Convert detection rules into formats supported by security platforms. |
| Alerting | ElastAlert | Generate alerts from matching Elasticsearch events. |
| Threat Intelligence | MITRE ATT&CK Navigator | Visualize and compare adversary techniques using ATT&CK layers. |
| Threat Emulation | Atomic Red Team | Provide controlled tests aligned with MITRE ATT&CK techniques. |

## Learning Outcomes

- Understand the objectives of NSM and ESM.
- Build sequential decoding recipes using CyberChef.
- Apply brute-force analysis to a controlled XOR challenge.
- Automate Morse code transformations and decoding.
- Organize incident response procedures in a malware playbook.
- Describe detection logic using Sigma.
- Convert detection rules into an alerting platform format.
- Compare threat group techniques using MITRE ATT&CK Navigator.

## Evidence Requirements

The original practical assignment consolidates the required evidence into a single PDF document.

[View Universal Class Evidence PDF](./evidences.pdf)

| Activity | Required Screenshot |
|---|---|
| 4.1 | Step 4 |
| 4.2 | Step 5 |
| 4.4 | Step 2 |
| 4.5 | Step 9 |

The written malware incident response playbook from Activity 4.3 is included in the same PDF, on pages 5–7.

## Technical Notes

- The XOR exercise uses a known plaintext prefix and a single-byte test key to recover a training flag.
- The Morse activity applies several transformations in sequence. Their order is important to obtain the expected decoded output.
- The Sigma exercise focuses on detecting the removal of the Linux immutable file attribute using chattr -i. The detection must be evaluated in the context of legitimate administrative activity.
- The APT3 and APT29 scores configured in Navigator are analytical values assigned for the exercise, not universal severity ratings for the groups.

## References

- [GCHQ CyberChef — Official Repository](https://github.com/gchq/CyberChef)
- [Sigma Rules Specification](https://sigmahq.io/sigma-specification/specification/sigma-rules-specification.html)
- [ElastAlert Documentation](https://elastalert.readthedocs.io/en/latest/ruletypes.html)
- [Uncoder IO](https://uncoder.io/)
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)
- [MITRE ATT&CK — APT3 (G0022)](https://attack.mitre.org/groups/G0022/)
- [MITRE ATT&CK — APT29 (G0016)](https://attack.mitre.org/groups/G0016/)
- [Atomic Red Team — T1222.002](https://github.com/redcanaryco/atomic-red-team/tree/master/atomics/T1222.002)

---

[Back to Module 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
