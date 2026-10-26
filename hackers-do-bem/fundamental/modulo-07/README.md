# Module 07 — Storage, Backup, and Data Erasure

> **Program:** Hackers do Bem  
> **Stage:** Fundamental  
> **Module:** 07  
> **Status:** Completed

## Overview

This module covers storage management, software RAID, file synchronization, cloud backups, local backups, filesystem formatting, and data overwriting techniques in Linux and Windows environments.

## Classes 25–26 — RAID and Backup Synchronization

| Activity | Topic | Description | |
|---|---|---|---|
| 7.01 | Software RAID 0 | Create and mount a RAID 0 array using `mdadm`. | [View](aula-25-26/atividade-7.01-raid-0-kali/README.md) |
| 7.02 | Software RAID 1 | Create and verify a mirrored RAID 1 array. | [View](aula-25-26/atividade-7.02-raid-1-kali/README.md) |
| 7.03 | Manual Rsync | Copy files between directories using `rsync`. | [View](aula-25-26/atividade-7.03-rsync-manual/README.md) |
| 7.04 | Automated Rsync with Cron | Automate directory synchronization with a scheduled cron job. | [View](aula-25-26/atividade-7.04-rsync-cron/README.md) |
| 7.05 | OneDrive Backup and Synchronization | Configure OneDrive folder backup on Windows Server 2022. | [View](aula-25-26/atividade-7.05-onedrive-backup/README.md) |

**Evidence:** [View PDF — Classes 25–26](aula-25-26/evidencias.pdf)

## Classes 27–28 — Local Backups and Data Erasure

| Activity | Topic | Description | |
|---|---|---|---|
| 7.06 | Local Full Backup with Duplicity | Create a local full backup and restore files for verification. | [View](aula-27-28/atividade-7.06-duplicity-backup-completo/README.md) |
| 7.07 | Local Differential Backup with Duplicity | Modify files, create a subsequent backup, and verify restoration. | [View](aula-27-28/atividade-7.07-duplicity-backup-diferencial/README.md) |
| 7.08 | Complete Formatting on Kali Linux | Recreate a filesystem and remove filesystem signatures using `wipefs`. | [View](aula-27-28/atividade-7.08-formatacao-completa/README.md) |
| 7.09 | Simple Data Overwriting | Demonstrate low-level overwriting with random data using `dd`. | [View](aula-27-28/atividade-7.09-sobrescrita-simples/README.md) |
| 7.10 | DoD 5220.22-M Overwrite Pattern | Use `shred` for a pseudorandom-data pass followed by a zero-fill pass. | [View](aula-27-28/atividade-7.10-sobrescrita-dod/README.md) |

**Evidence:** [View PDF — Classes 27–28](aula-27-28/evidencias.pdf)

## Key Skills Practiced

- Software RAID configuration and verification.
- File synchronization with `rsync`.
- Task scheduling and automation with `cron`.
- Cloud backup configuration using OneDrive.
- Local backup and restoration using Duplicity.
- Linux partition and filesystem management.
- Filesystem signature removal using `wipefs`.
- Data overwriting techniques and their limitations.

> **Security note:** Formatting partitions, removing filesystem signatures, and overwriting block devices are destructive operations. Perform them only on authorized lab devices. Overwriting does not guarantee secure data erasure on every storage medium.

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Repository](../../../README.md)
