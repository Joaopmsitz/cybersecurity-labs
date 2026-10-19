# HTB Academy — Module Library

> Centralized technical documentation for HTB Academy modules.

This library contains reusable technical notes, commands, workflows, and practical exercises organized by cybersecurity domain.

## Knowledge Domains

| Domain | Focus |
|---|---|
| [Academy Basics](./academy-basics/) | Platform orientation and foundational concepts |
| [Defensive](./defensive/) | Security monitoring, detection, and incident response |
| [Networking](./networking/) | Network concepts, protocols, and traffic analysis |
| [Password Attacks](./password-attacks/) | Password cracking and authentication attacks |
| [Reconnaissance](./reconnaissance/) | Information gathering, scanning, and enumeration |
| [Web](./web/) | HTTP, JavaScript, web assessment, and related tools |

Domains reflect the primary subject of each module, not the learning path in which it appears.

## Documentation Structure

Each module has its own directory:

```text
module-name/
├── README.md
├── images/   # Screenshots and supporting images, when needed
└── labs/     # Individual lab notes, when relevant$ErrorActionPreference = "Stop"

Set-Location "C:\GitHub\cybersecurity-labs"

$relativePath = "hackthebox/academy/modules/README.md"
$readme = Join-Path (Get-Location).Path $relativePath
$utf8 = New-Object System.Text.UTF8Encoding($false)

# Evitar misturar arquivos previamente preparados no Git.
$staged = @(git diff --cached --name-only)
if ($LASTEXITCODE -ne 0) {
    throw "Falha ao verificar o staging do Git."
}
if ($staged.Count -gt 0) {
    $staged | ForEach-Object { Write-Host "Staged: $_" }
    throw "Existem arquivos staged. Resolva essas alterações antes de continuar."
}

# Confirmar que os domínios já existem.
$domains = @(
    "academy-basics",
    "defensive",
    "networking",
    "password-attacks",
    "reconnaissance",
    "web"
)

foreach ($domain in $domains) {
    $domainPath = Join-Path (Get-Location).Path "hackthebox/academy/modules/$domain"
    if (!(Test-Path $domainPath -PathType Container)) {
        throw "Diretório não encontrado: $domainPath"
    }
}

# README curto, sem repetir o conteúdo do índice geral da Academy.
$content = @'
# HTB Academy — Module Library

> Centralized technical documentation for HTB Academy modules.

This directory contains reusable technical notes, commands, workflows, and practical exercises organized by cybersecurity domain.

## Knowledge Domains

| Domain | Focus |
|---|---|
| [Academy Basics](./academy-basics/) | Platform orientation and foundational concepts |
| [Defensive](./defensive/) | Security monitoring, detection, and incident response |
| [Networking](./networking/) | Network protocols, concepts, and traffic analysis |
| [Password Attacks](./password-attacks/) | Password cracking and authentication attacks |
| [Reconnaissance](./reconnaissance/) | Information gathering, scanning, and enumeration |
| [Web](./web/) | HTTP, JavaScript analysis, web assessment, and security tools |

Domains represent the primary subject of a module, not the learning path where it appears.

## Module Structure

- `README.md` — concise technical reference with reusable concepts, commands, workflows, and lessons learned.
- `images/` — screenshots and supporting images referenced in the documentation.
- `labs/` — separate notes for relevant practical exercises.

Create `images/` and `labs/` only when needed.

## Documentation Principles

- **One module, one location:** maintain a single technical reference for each module.
- **Organize by domain:** classify modules by their primary technical subject.
- **Link instead of duplicating:** learning paths reference existing module documentation.
- **Prioritize practical value:** document useful findings and workflows instead of reproducing Academy lessons.

## Navigation

- [HTB Academy Overview](../README.md)
- [All Learning Paths](../paths/README.md)
- [Job Role Paths](../paths/job-role/README.md)
- [Skill Paths](../paths/skill/README.md)
- [HTB Academy](https://academy.hackthebox.com/)
