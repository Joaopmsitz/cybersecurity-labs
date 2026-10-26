# Activity 7.08 — Complete Formatting on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 27–28  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Prepare and format a partition on Kali Linux by removing the previous RAID configuration, recreating the filesystem, and finally removing filesystem signatures using `wipefs`.

The lab uses the disk `/dev/nvme1n1`, which does not contain the virtual machine's primary operating system.

## Environment

- **Operating system:** Kali Linux
- **Disk used:** `/dev/nvme1n1`
- **Partition:** `/dev/nvme1n1p1`
- **Tools:** `mdadm`, `fdisk`, `partprobe`, `mkfs.ext4`, and `wipefs`

> The operations described below are destructive and were performed only on the disk provided for the lab.

## 1. Switching to the Root User

Administrative access was obtained:

```bash
sudo -i
```

## 2. Identifying the Disks

The `fdisk -l` command was used to identify the available disks and partitions:

```bash
fdisk -l
```

Output recorded during the lab:

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
/dev/nvme1n1p3      411648 616447  204800  100M 83 Linux
/dev/nvme1n1p4      616448 821247  204800  100M 83 Linux
```

The disk used in the lab is `/dev/nvme1n1`, while the operating system is installed on `/dev/nvme0n1`.

## 3. Stopping the RAID Device

Because the secondary disk had been used for RAID arrays in previous activities, the following command was run:

```bash
mdadm --stop /dev/nvme1n1
```

The purpose of this step is to stop the RAID configuration before cleaning and modifying the partitions.

## 4. Removing RAID Metadata

To remove RAID superblock signatures from the four existing partitions, the following commands were executed:

```bash
mdadm --zero-superblock /dev/nvme1n1p1
mdadm --zero-superblock /dev/nvme1n1p2
mdadm --zero-superblock /dev/nvme1n1p3
mdadm --zero-superblock /dev/nvme1n1p4
```

The `mdadm --zero-superblock` command removes the superblock metadata used by RAID, allowing the partitions to stop being identified as members of the previous array.

## 5. Deleting the Existing Partitions

The disk partitioning utility was opened:

```bash
fdisk /dev/nvme1n1
```

Partitions `p4`, `p3`, and `p2` were deleted, initially leaving `p1` in place.

Recorded output:

```text
Welcome to fdisk (util-linux 2.41.2).                                                                      
Changes will remain in memory only, until you decide to write them.                                        
Be careful before using the write command.

Command (m for help): d
Partition number (1-4, default 4): 

Partition 4 has been deleted.

Command (m for help): d
Partition number (1-3, default 3): 

Partition 3 has been deleted.

Command (m for help): d
Partition number (1,2, default 2): 

Partition 2 has been deleted.

Command (m for help): p
Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xf8a2dbef

Device         Boot Start    End Sectors  Size Id Type
/dev/nvme1n1p1       2048 206847  204800  100M 83 Linux

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

After the changes, the following command was executed:

```bash
partprobe /dev/nvme1n1
```

`partprobe` asks the kernel to reread the updated partition table.

## 6. Formatting the Partition

With the `nvme1n1p1` partition available, a new ext4 filesystem was created:

```bash
mkfs.ext4 /dev/nvme1n1p1
```

Output:

```text
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 102400 1k blocks and 25584 inodes
Filesystem UUID: 61378c9f-f4b6-4231-afc1-6d3a753cef94
Superblock backups stored on blocks: 
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

The `mkfs.ext4` command created a new ext4 filesystem structure on the partition.

## 7. Removing Filesystem Signatures

After formatting, `wipefs` was used to remove the recognized filesystem signatures:

```bash
wipefs -a /dev/nvme1n1p1
```

Output:

```text
/dev/nvme1n1p1: 2 bytes were erased at offset 0x00000438 (ext4): 53 ef
```

The output indicates that `wipefs` identified an ext4 signature at offset `0x00000438` and removed the corresponding two bytes (`53 ef`).

The `-a` parameter requests the removal of all recognized filesystem signatures on the device.

> **Note:** `wipefs -a` removes signatures and identifying filesystem metadata. It should not be interpreted as a secure method for erasing all existing data from a device.

## Evidence

The evidence requested for this activity corresponds to step 7, documenting the execution of `wipefs` and the removal of the ext4 signature.

Evidence for this activity is included in the PDF for Module 7, Classes 27–28.

[View Evidence — Classes 27–28](../evidencias.pdf)

---

[Back to Classes 27–28](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
