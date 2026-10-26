# Activity 12.09 — Exploring The Sleuth Kit (TSK) on Kali Linux

This activity introduces **The Sleuth Kit (TSK)** on Kali Linux, using forensic analysis commands to examine a partition and its inodes.

> **Note:** Credentials used in the lab environment are not recorded in this document.

## Objective

- Identify available disk partitions.
- Use The Sleuth Kit tools.
- List files and directories within a partition.
- Query information related to inodes and their timestamps.

## Procedure

### 1. Accessing Kali Linux

Kali Linux was accessed via RDP using the address `192.168.98.40`.

Administrative privileges were obtained using:

```bash
sudo -i
```

### 2. Identifying Disks and Partitions

The following command was used:

```bash
fdisk -l
```

Output:

```text
Disk /dev/nvme0n1: 22 GiB, 23622320128 bytes, 46137344 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: 9FFA977A-4F2F-44A0-BCAC-15A77352798A

Device           Start      End  Sectors  Size Type
/dev/nvme0n1p1  262144 46137310 45875167 21,9G Linux filesystem
/dev/nvme0n1p14   2048     8191     6144    3M BIOS boot
/dev/nvme0n1p15   8192   262143   253952  124M EFI System

Partition table entries are not in disk order.


Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xf8a2dbef

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux
/dev/nvme1n1p3      411648 821247  409600  200M 83 Linux

```

The main partition used by the system is:

```text
/dev/nvme0n1p1
```

### 3. Understanding Inodes

In Linux, an **inode** is a structure used by the filesystem to store information about a file or directory, such as its identifier, permissions, owner, size, and timestamps.

In forensic analysis, inode information can help reconstruct events associated with files.

### 4. Listing Files with `fls`

The following command was used:

```bash
fls /dev/nvme0n1p1
```

Output:

```text
d/d 524461:     home
d/d 11:         lost+found
d/d 131073:     boot
d/d 396737:     curso
d/d 524289:     var
d/d 393229:     etc
d/d 131075:     usr
l/l 13:         bin
d/d 524460:     dev
l/l 14:         lib
d/d 524463:     proc
d/d 524464:     root
d/d 524465:     run
l/l 16:         sbin
d/d 393258:     sys
l/l 15:         lib64
d/d 524467:     tmp
d/d 524556:     mnt
d/d 524557:     srv
d/d 524558:     opt
d/d 524560:     media
r/r 64113:      .autorelabel
d/d 410038:     snap
V/V 1433601:    $OrphanFiles

```

The `fls` command lists files and directories found in the filesystem and associates them with their respective inode identifiers.

The following entry was also observed:

```text
V/V 1433601:    $OrphanFiles

```

This indicates the presence of structures associated with orphaned files identified by TSK.

### 5. Querying Inode Information

The following command was executed:

```bash
ils /dev/nvme0n1p1 2
```

Output:

```text
class|host|device|start_time
ils|kali||1765063051
st_ino|st_alloc|st_uid|st_gid|st_mtime|st_atime|st_ctime|st_crtime|st_mode|st_nlink|st_size

```

The value `1765063051` corresponds to the time when the collection started. The timestamp was converted using:

```bash
date -d @1765063051
```

Result:

```text
sáb 06 dez 2025 20:17:31 -03

```

The `ils` output presents fields related to inodes, including:

- **`st_ino`:** Inode number.
- **`st_alloc`:** Information about inode allocation.
- **`st_uid`:** User ID of the owner.
- **`st_gid`:** Group ID.
- **`st_mtime`:** Modification timestamp.
- **`st_atime`:** Access timestamp.
- **`st_ctime`:** Metadata change timestamp.
- **`st_crtime`:** Creation timestamp, when supported by the filesystem.
- **`st_mode`:** File type and permissions.
- **`st_nlink`:** Number of links.
- **`st_size`:** Size associated with the inode.

## Key Concepts

- **The Sleuth Kit (TSK):** A collection of tools for forensic analysis of filesystems and storage media.
- **`fls`:** Lists files and directories identified in a disk image or filesystem.
- **`ils`:** Displays information related to inodes.
- **Inode:** A structure that stores file and directory metadata.
- **Timestamps:** Temporal information that is important for event analysis.

## Activity Workflow

```text
Partition
   ↓
fdisk -l
   ↓
Identify /dev/nvme0n1p1
   ↓
fls
   ↓
List files and directories
   ↓
ils
   ↓
Inode information and timestamps
```

## Result

The TSK tools were used to list filesystem structures and query inode-related information, providing an introduction to forensic analysis of Linux filesystems.

## Evidence

[**View Evidence — Module 12 / Classes 47–48**](../evidencias.pdf)

**Required screenshot:** Step 5 — output of `ils /dev/nvme0n1p1 2`.

---

[Back to Classes 47–48](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
