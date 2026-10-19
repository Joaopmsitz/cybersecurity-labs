# 🎓 HTB Academy

Personal knowledge base for Hack The Box Academy.

This directory is organized by cybersecurity knowledge domains, with a centralized library of HTB Academy modules and separate indexes for official HTB learning paths.

## 📚 Module Library

The `modules/` directory contains the actual technical documentation for individual HTB Academy modules, including notes, commands, procedures, lab write-ups, screenshots, and lessons learned.

Each module is documented in one location, regardless of how many HTB Paths include it.

### Knowledge Domains

Modules are grouped by their primary subject rather than the learning path where they were completed.

- `academy-basics/` — HTB Academy orientation, platform fundamentals, and introductory concepts
- `networking/` — Network concepts, protocols, traffic analysis, and network tooling
- `reconnaissance/` — Information gathering, host discovery, scanning, and enumeration
- `web/` — Web technologies, HTTP requests, JavaScript analysis, web attacks, proxies, and web security tooling
- `password-attacks/` — Password cracking, brute-force attacks, and password-based authentication weaknesses
- `exploitation/` — Vulnerability exploitation, exploit development concepts, and offensive frameworks
- `privilege-escalation/` — Linux and Windows privilege escalation techniques
- `post-exploitation/` — Post-compromise discovery, credential access, persistence, and lateral movement, excluding modules primarily focused on privilege escalation
- `active-directory/` — Active Directory enumeration, attacks, domain environments, and security concepts
- `defensive/` — Blue Team operations, detection engineering, SIEM, monitoring, incident response, and security analysis
- `forensics/` — Digital forensics, evidence acquisition, investigation, and artifact analysis
- `cloud/` — Cloud infrastructure, services, security, and attack techniques

These domains are organizational categories, not a mandatory learning sequence. New categories should be created only when needed, and modules should be assigned to the domain that best represents their primary subject.

## 🛣️ HTB Paths

The `paths/` directory tracks official HTB Academy learning paths associated with the modules documented in this repository.

Paths serve as indexes and progress trackers rather than as a second copy of the technical content.

- `paths/skill/` — HTB Skill Paths
- `paths/job-role/` — HTB Job Role Paths

Each path README may document the path overview, module order, difficulty, progress, completion status, badge, and other path-specific information.

Module entries link to the corresponding README in `modules/`. If multiple paths contain the same module, they all reference the same documentation.

## 📝 Module Documentation

Each documented module has its own directory under the appropriate knowledge domain.

A typical module directory follows this structure:

```text
module-name/
├── README.md
├── images/
└── labs/
```

- `README.md` — Concise technical reference containing key concepts, commands, workflows, configuration, techniques, troubleshooting, references, and relevant lessons learned
- `images/` — Screenshots and supporting images referenced by the documentation
- `labs/` — Individual lab notes, practical exercises, and detailed walkthroughs when necessary

Create `images/` and `labs/` when needed rather than requiring empty directories for every module.

The module README should prioritize reusable technical knowledge rather than reproduce the Academy's lesson content or simply record course completion.

## 🔗 Documentation Principles

1. **One module, one location.** Technical notes, labs, and screenshots belong to the module's directory.
2. **Organize by subject.** Categorize modules according to their primary technical focus, not by their official HTB Path or difficulty level.
3. **Link instead of duplicating.** Skill Paths and Job Role Paths reference the centralized module documentation.
4. **Keep path-specific information separate.** Path overviews, progress, completion dates, and path badges belong to their respective path README files.
5. **Document incrementally.** Add notes and lab files as practical work progresses; do not create unnecessary scaffolding or duplicate documentation.
6. **Preserve existing work.** Reorganize directories and update links without rewriting completed notes or unnecessarily moving screenshots between modules.

The objective is to build a reusable technical reference that remains useful beyond any individual HTB Academy course or learning path.

## 📂 Structure

```text
academy/
├── README.md
│
├── modules/
│   ├── academy-basics/
│   │   ├── getting-started/
│   │   └── introduction-to-academy/
│   │
│   ├── networking/
│   │   └── intro-to-network-traffic-analysis/
│   │
│   ├── reconnaissance/
│   │   └── network-enumeration-with-nmap/
│   │
│   ├── web/
│   │   ├── web-requests/
│   │   ├── javascript-deobfuscation/
│   │   ├── attacking-web-applications-with-ffuf/
│   │   ├── sqlmap-essentials/
│   │   └── using-web-proxies/
│   │
│   ├── password-attacks/
│   │   ├── cracking-passwords-with-hashcat/
│   │   └── login-brute-forcing/
│   │
│   ├── exploitation/
│   ├── privilege-escalation/
│   ├── post-exploitation/
│   ├── active-directory/
│   ├── defensive/
│   │   ├── incident-handling-process/
│   │   └── security-monitoring-siem-fundamentals/
│   ├── forensics/
│   └── cloud/
│
└── paths/
    ├── README.md
    ├── skill/
    │   ├── README.md
    │   ├── basic-toolset/
    │   │   └── README.md
    │   └── cracking-into-hack-the-box/
    │       └── README.md
    │
    └── job-role/
        ├── README.md
        └── soc-analyst/
            └── README.md
```

The tree illustrates the intended organization; create domain directories as relevant modules are documented. Individual module directories may contain their own `README.md`, `images/`, and `labs/` as needed.
