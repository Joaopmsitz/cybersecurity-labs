# 🎓 HTB Academy

Personal knowledge base for Hack The Box Academy.

This directory is organized around cybersecurity domains rather than HTB Paths.

## 📚 Knowledge Domains

The domain folders contain the actual technical notes, practical procedures, commands, and lessons learned from HTB Academy modules.

The general learning flow is:

1. Fundamentals
2. Reconnaissance
3. Networking / Web
4. Exploitation
5. Post-Exploitation
6. Active Directory

Defensive security is maintained as a separate domain because its concepts are not limited to a single stage of the offensive workflow.

### Domains

- `fundamentals/` — Core cybersecurity and operating system concepts
- `reconnaissance/` — Information gathering and enumeration
- `networking/` — Network concepts, protocols, traffic analysis, and related tooling
- `web/` — Web technologies, requests, attacks, and web security tooling
- `exploitation/` — Exploitation techniques and offensive frameworks
- `post-exploitation/` — Privilege escalation, credential access, discovery, lateral movement, and related techniques
- `active-directory/` — Active Directory enumeration, attacks, and security concepts
- `defensive/` — Defensive security, detection, monitoring, and analysis

## 🛣️ HTB Paths

The `paths/` directory tracks the HTB learning paths associated with the modules documented in this repository.

Paths are used as indexes and progress trackers rather than as a second copy of the technical content.

- `paths/skill/` — HTB Skill Paths
- `paths/job-role/` — HTB Job Role Paths

A module is documented only once in its relevant knowledge domain. Paths link back to that module instead of duplicating its content.

## 📝 Module Documentation

Each completed module should contain a dedicated `README.md` with practical notes such as:

- Concepts learned
- Tools and commands
- Practical workflows
- Configuration steps
- Important techniques
- Troubleshooting
- Useful references
- Personal observations

The goal is to build a practical reference that can be revisited later, rather than simply recording module completion.

## 🔗 Structure

```text
academy/
├── fundamentals/
├── reconnaissance/
├── networking/
├── web/
├── exploitation/
├── post-exploitation/
├── active-directory/
├── defensive/
│
└── paths/
    ├── skill/
    └── job-role/