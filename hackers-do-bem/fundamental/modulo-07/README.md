# Module 07 — Storage, Backup, and Data Erasure

> **Program:** Hackers do Bem  
> **Stage:** Fundamental  
> **Module:** 07  
> **Status:** Completed

## Overview

This module covers storage management, software RAID, file synchronization, cloud backups, local backups, filesystem formatting, and data overwriting techniques using Linux and Windows environments.

The activities are organized into two class groups:

- **Classes 25–26:** RAID configuration, file synchronization, and OneDrive backup.
- **Classes 27–28:** Local backups with Duplicity, filesystem formatting, and data overwriting.

## Classes 25–26 — RAID and Backup Synchronization

| Activity | Topic | Description |
|---|---|---|
| [7.01 — Software RAID 0](aula-25-26/atividade-7.01-raid-0-kali/README.md) | Kali Linux | Create and mount a RAID 0 array using `mdadm`. |
| [7.02 — Software RAID 1](aula-25-26/atividade-7.02-raid-1-kali/README.md) | Kali Linux | Create and verify a mirrored RAID 1 array. |
| [7.03 — Manual Rsync](aula-25-26/atividade-7.03-rsync-manual/README.md) | Linux | Copy files between directories using `rsync`. |
| [7.04 — Automated Rsync with Cron](aula-25-26/atividade-7.04-rsync-cron/README.md) | Linux | Automate directory synchronization with a scheduled cron job. |
| [7.05 — OneDrive Backup and Synchronization](aula-25-26/atividade-7.05-onedrive-backup/README.md) | Windows Server 2022 | Configure OneDrive and enable folder backup and cloud synchronization. |

[View Evidence — Classes 25–26](aula-25-26/evidencias.pdf)

## Classes 27–28 — Local Backups and Data Erasure

| Activity | Topic | Description |
|---|---|---|
| [7.06 — Local Full Backup with Duplicity](aula-27-28/atividade-7.06-duplicity-backup-completo/README.md) | Kali Linux | Create a local full backup and restore files for verification. |
| [7.07 — Local Differential Backup with Duplicity](aula-27-28/atividade-7.07-duplicity-backup-diferencial/README.md) | Kali Linux | Modify files, create a subsequent backup, and verify restoration. |
| [7.08 — Complete Formatting](aula-27-28/atividade-7.08-formatacao-completa/README.md) | Kali Linux | Manage partitions, recreate a filesystem, and remove filesystem signatures using `wipefs`. |
| [7.09 — Simple Data Overwriting](aula-27-28/atividade-7.09-sobrescrita-simples/README.md) | Kali Linux | Demonstrate low-level overwriting with random data using `dd`. |
| [7.10 — DoD 5220.22-M Overwrite Pattern](aula-27-28/atividade-7.10-sobrescrita-dod/README.md) | Kali Linux | Use `shred` to perform a pseudorandom-data pass followed by a zero-fill pass. |

[View Evidence — Classes 27–28](aula-27-28/evidencias.pdf)

## Key Skills Practiced

- Software RAID configuration and status verification.
- File synchronization with `rsync`.
- Task scheduling and automation with `cron`.
- Cloud backup configuration using OneDrive.
- Local backup and restoration using Duplicity.
- Linux partition and filesystem management.
- Filesystem signature removal with `wipefs`.
- Data overwriting concepts and the limitations of overwrite-based erasure.

> **Security note:** Partition formatting, filesystem signature removal, and direct block-device overwriting are destructive operations. They should only be performed on explicitly authorized lab devices. Overwriting does not guarantee secure erasure on every type of storage media.

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Repository](../../../README.md)
