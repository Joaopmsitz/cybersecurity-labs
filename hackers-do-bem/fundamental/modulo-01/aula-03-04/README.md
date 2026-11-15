# Hackers do Bem — Fundamental | Module 01 — Classes 03–04

Documentation of the practical activities from Classes 03–04 of Module 01 of the Hackers do Bem Fundamental training stage.

These classes explore phishing awareness in a controlled laboratory, domain registration reconnaissance, Maltego installation and graph analysis, Open-Source Intelligence (OSINT), and adversarial machine learning applied to image classification.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Fundamental |
| Module | 01 |
| Classes | 03–04 |
| Activities | 5 |
| Main Topics | Phishing, WHOIS, OSINT, Maltego, Domain Intelligence, and Adversarial Machine Learning |
| Environment | Activity-specific laboratory and analysis tools |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 1.6 — Phishing Simulation with ShellPhish | Social Engineering | Explore phishing techniques through a controlled local-lab simulation using ShellPhish. | [View Activity](./atividade-1.6-phishing/README.md) |
| 1.7 — Domain Registration Reconnaissance with WHOIS | Domain Intelligence | Investigate publicly available domain registration information and understand the data returned by WHOIS queries. | [View Activity](./atividade-1.7-whois/README.md) |
| 1.8 — Maltego Installation and Data Hub Exploration | OSINT Tools | Explore Maltego installation, authentication, and the Data Hub integration environment. | [View Activity](./atividade-1.8-maltego/README.md) |
| 1.9 — OSINT Investigation and Relationship Mapping with Maltego | Open-Source Intelligence | Collect public-source information and visualize relationships between entities through Maltego graphs and transforms. | [View Activity](./atividade-1.9-osint/README.md) |
| 1.10 — Adversarial Machine Learning and Image Classification | Artificial Intelligence Security | Explore adversarial machine learning concepts and their impact on image classification models. | [View Activity](./atividade-10-adversarial-ml/README.md) |

## Environment

The activities use different environments and analysis contexts rather than a single uniform lab setup.

| Activity | Environment |
|---|---|
| 1.6 | Controlled local laboratory for phishing simulation. |
| 1.7 | Domain registration lookup and public information sources. |
| 1.8 | Maltego application, authentication, and Data Hub. |
| 1.9 | OSINT research environment and Maltego graph analysis. |
| 1.10 | Image classification and adversarial machine learning exercise environment. |

Refer to each activity README for its specific operating system, software configuration, and procedure.

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Phishing Simulation | ShellPhish | Explore phishing techniques in a controlled and authorized local laboratory. |
| Domain Intelligence | WHOIS, RDAP | Retrieve and investigate domain registration information. |
| OSINT Platform | Maltego | Collect, correlate, and visualize information about related entities. |
| Data Integration | Maltego Data Hub | Explore integrations and data providers available through Maltego. |
| Graph Analysis | Maltego Transforms | Expand investigations by retrieving information related to selected entities. |
| Artificial Intelligence Security | Image Classification, Adversarial Examples | Understand how input perturbations can affect model classification results. |

## Learning Outcomes

- Recognize phishing techniques and understand their security implications.
- Explore phishing simulations in a controlled laboratory environment.
- Understand domain registration reconnaissance and the limitations of registration data.
- Explore WHOIS and the transition toward RDAP.
- Install and authenticate to Maltego.
- Understand the purpose of Maltego Data Hub and Transforms.
- Collect and correlate information from public sources.
- Visualize relationships between entities through graph-based investigations.
- Understand adversarial examples and their effect on image classification models.
- Recognize the importance of validating information collected through OSINT.

## Evidence Requirements

The practical activities are documented in a single PDF for the Classes 03–04 group.

[View Class Evidence PDF](./evidencias.pdf)

The evidence file consolidates the supporting material for the five activities.

## Technical Notes

- Phishing simulation tools must be restricted to authorized, isolated training environments. The activity should not be used to target real users or collect credentials outside the approved laboratory scope.
- WHOIS is the traditional domain registration query protocol. ICANN identifies RDAP as its replacement for most generic top-level domain registration data. Since January 28, 2025, gTLD registries and registrars are no longer generally required to provide WHOIS services, with exceptions including `.com`, `.name`, and `.post`.
- Maltego Transforms retrieve related information for entities and add the results to graph-based investigations. The availability of data providers and transforms depends on the configured account and integrations.
- OSINT results should be evaluated in context. Publicly available information may be outdated, incomplete, or inaccurate and should be corroborated whenever possible.
- Adversarial examples demonstrate that carefully crafted changes to model inputs can cause image classifiers to produce incorrect predictions. Results depend on the model, attack method, and perturbation parameters.

## References

- [NIST SP 800-50 Rev. 1 — Building a Cybersecurity and Privacy Learning Program](https://csrc.nist.gov/pubs/sp/800/50/r1/final)
- [ICANN — Registration Data Access Protocol (RDAP)](https://www.icann.org/en/contracted-parties/registry-operators/resources/registration-data-access-protocol)
- [ICANN — Launching RDAP and Sunsetting WHOIS](https://www.icann.org/en/announcements/details/icann-update-launching-rdap-sunsetting-whois-27-01-2025-en)
- [IETF RFC 3912 — WHOIS Protocol Specification](https://datatracker.ietf.org/doc/html/rfc3912)
- [Maltego — What Is Maltego?](https://support.maltego.com/en/support/solutions/articles/15000019166-what-is-maltego-)
- [Maltego — Running Transforms](https://docs.maltego.com/en/support/solutions/articles/15000009613-running-transforms)
- [Maltego — Data Hub](https://docs.maltego.com/en/support/solutions/articles/15000010778-the-transform-hub)
- [PyTorch — Adversarial Example Generation](https://docs.pytorch.org/tutorials/beginner/fgsm_tutorial.html)

---

[Back to Module 01](../README.md) · [Back to Fundamental](../../README.md) · [Back to Hackers do Bem](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
