# Hackers do Bem - Specialization | Module 02 - Class 09

This class covers forensic preparation, physical and logical evidence acquisition, filesystem analysis, file recovery, and partition recovery.

The practical activities use Debian, The Sleuth Kit, Foremost, Magic Rescue, Hexedit, and standard Linux forensic utilities.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 02 - Data Processing |
| Class | 09 |
| Main Topic | Preparation, Collection, and Recovery of Disk Data |
| Main Technologies | Debian, The Sleuth Kit, Foremost, Magic Rescue, Hexedit |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 9.1 | Preparing a Forensic Toolkit | Prepare bootable Debian media and an external forensic workstation with analysis tools. | [View Activity](./atividade-9.1-preparacao-ferramenta-forense/README.md) |
| 9.2 | Collecting Physical Evidence | Create a bit-by-bit disk image and verify its integrity using cryptographic hashes. | [View Activity](./atividade-9.2-coleta-evidencias-fisicas/README.md) |
| 9.3 | Analyzing the Disk and Filesystem | Examine disk metadata, filesystem characteristics, volume labels, sectors, and directory entries. | [View Activity](./atividade-9.3-analise-disco-filesystem/README.md) |
| 9.4 | Collecting Logical Evidence | Mount a forensic image read-only, inspect file metadata, and recover embedded files. | [View Activity](./atividade-9.4-coleta-evidencias-logicas/README.md) |
| 9.5 | Recovering Partitions and Data | Locate filesystem offsets in a damaged disk image and recover access to partition contents. | [View Activity](./atividade-9.5-recuperacao-particoes-dados/README.md) |

## Environment

Activities 9.1 and 9.2 use physical storage devices and a separately prepared Debian forensic environment.

Activities 9.3, 9.4, and 9.5 use the supplied `forenseLinux` virtual machine and training disk images.

| Component | Purpose |
|---|---|
| Debian | Forensic workstation operating system |
| The Sleuth Kit | Filesystem and disk image examination |
| `fdisk` | Disk and partition information |
| `hwinfo` | Hardware and storage device identification |
| `dd` | Bit-by-bit disk acquisition |
| `md5sum` | MD5 checksum calculation |
| `sha256sum` | SHA-256 checksum calculation |
| `fls` | File and directory listing from forensic images |
| `fsstat` | Filesystem metadata and structural information |
| `foremost` | File carving and recovery |
| `hexedit` | Hexadecimal inspection |
| `strings` | Text extraction from binary files |
| `pdfinfo` | PDF metadata inspection |
| `exiftool` | Metadata extraction |

## Tools and Technologies

- Debian GNU/Linux
- The Sleuth Kit (TSK)
- `dd`
- MD5 and SHA-256
- `fdisk`
- `hwinfo`
- `fls`
- `fsstat`
- `foremost`
- `magicrescue`
- `hexedit`
- `file`
- `stat`
- `strings`
- `pdfinfo`
- `exiftool`

## Learning Outcomes

- Prepare a portable forensic workstation.
- Identify physical storage devices and partitions.
- Acquire bit-by-bit disk images.
- Verify image integrity using cryptographic hashes.
- Identify filesystem types and volume metadata.
- Enumerate files and directories within forensic images.
- Mount forensic images in read-only mode.
- Inspect file metadata and embedded content.
- Recover deleted or embedded files using file carving.
- Identify filesystem offsets in damaged disk images.
- Recover access to data stored in previously unidentified partitions.

## Evidence

A single PDF contains the screenshots required for Activities 9.3, 9.4, and 9.5.

| Activity | Required Step | Evidence Description | PDF Page |
|---|---|---|---|
| 9.3 | Step 7 | `fls` output listing files and directory paths identified inside `pendrive.dd`. | 1 |
| 9.4 | Step 6 | Foremost command and the recovered JPG image displayed successfully. | 2 |
| 9.5 | Step 6 | `resultado.txt` showing detected filesystem offsets, including sector 2048 and Ext2 filesystem information. | 3 |

- [View consolidated evidence - evidences.pdf](./evidences.pdf)

Activities 9.1 and 9.2 do not require screenshots for this practical submission.

## Important Safety Notes

- Activities 9.1 and 9.2 must be performed using physical storage devices and the student's own physical workstation.
- Do not attempt Activities 9.1 or 9.2 inside the course virtual machine.
- Installing an operating system on an external device and acquiring physical disks can cause irreversible data loss if the wrong device is selected.
- Confirm source and destination devices before running any acquisition command.
- Use a hardware write blocker when available and preserve the original evidence.
- Perform filesystem analysis on forensic copies rather than modifying original evidence.
- Mount forensic images read-only whenever the task only requires examination.

## Technical Notes

- The Sleuth Kit provides utilities for examining disk images and filesystem structures.
- `fls` lists files and directory entries from a forensic image.
- `fsstat` displays filesystem metadata and structural information.
- The `dd` command copies data from its input (`if`) to its output (`of`); selecting these paths incorrectly can overwrite valuable data.
- The original course hash-comparison example contains an incorrect redirection. The correct `diff` syntax compares two existing files as separate arguments.
- Hash comparison should compare digest values, not the filenames embedded in the default checksum output.
- Read-only mounting helps preserve evidence during logical examination.
- The partition recovery exercise uses a sector offset multiplied by the sector size to locate a filesystem within a raw image.

## References

- [Debian - Network Installation](https://www.debian.org/CD/netinst/)
- [Rufus - Official Website](https://rufus.ie/)
- [The Sleuth Kit - fls](https://manpages.debian.org/trixie/sleuthkit/fls.1.en.html)
- [The Sleuth Kit - fsstat](https://manpages.debian.org/trixie/sleuthkit/fsstat.1.en.html)
- [The Sleuth Kit - Tool Overview](https://github.com/sleuthkit/sleuthkit/wiki/TSK_Tool_Overview)
- [GNU Coreutils - dd](https://www.gnu.org/software/coreutils/manual/coreutils.html)
- [Linux - diff manual](https://man7.org/linux/man-pages/man1/diff.1.html)
- [Linux - mount manual](https://man7.org/linux/man-pages/man8/mount.8.html)

## Navigation

- [Module 02](../README.md)
- [Previous Class - 08](../aula-08/README.md)
- [Next Class - 10](../aula-10/README.md)
- [Specialization Overview](../../README.md)
