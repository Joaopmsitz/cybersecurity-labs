# Activity 7.02 — Implementing Software RAID 1 on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 25–26  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Implement a Software RAID 1 array on Kali Linux using two new 100 MiB partitions on the secondary disk `/dev/nvme1n1`.

RAID 1 uses mirroring, maintaining a copy of the data on each device that makes up the array. In this lab, the array is created with `mdadm`, formatted with ext4, and mounted at `/mnt/raid1`.

This activity reuses the same secondary disk used in the previous RAID 0 activity, creating the partitions `/dev/nvme1n1p3` and `/dev/nvme1n1p4`.

## 1. Checking Existing Disks and Arrays

First, the `fdisk -l` command was used to check the current disk configuration and the arrays created previously.

```text
┌──(root㉿kali)-[~]
└─# fdisk -l

Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x9c63bfb2

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux


Disk /dev/nvme0n1: 19 GiB, 20401094656 bytes, 39845888 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: 9FFA977A-4F2F-44A0-BCAC-15A77352798A

Device           Start      End  Sectors  Size Type
/dev/nvme0n1p1  262144 39845854 39583711 18,9G Linux filesystem
/dev/nvme0n1p14   2048     8191     6144    3M BIOS boot
/dev/nvme0n1p15   8192   262143   253952  124M EFI System

Partition table entries are not in disk order.


Disk /dev/md0: 196 MiB, 205520896 bytes, 401408 sectors
Disk model:
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 524288 bytes / 1048576 bytes
```

The disk `/dev/nvme1n1` already contained the two 100 MiB partitions used in the previous activity:

- `/dev/nvme1n1p1`
- `/dev/nvme1n1p2`

The `/dev/md0` array, corresponding to the previously created RAID 0, was also present.

The new RAID 1 partitions would be created from the available space after `/dev/nvme1n1p2`.

## 2. Creating the RAID 1 Partitions

The `fdisk` utility was used on the secondary disk:

```bash
fdisk /dev/nvme1n1
```

Two new primary partitions of 100 MiB each were created:

- `/dev/nvme1n1p3`
- `/dev/nvme1n1p4`

Procedure output:

```text
┌──(root㉿kali)-[~]
└─# fdisk /dev/nvme1n1

Welcome to fdisk (util-linux 2.40.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

This disk is currently in use - repartitioning is probably a bad idea.
It's recommended to umount all file systems, and swapoff all swap
partitions on this disk.

Command (m for help): n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (3,4, default 3):
First sector (411648-4194303, default 411648):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (411648-4194303, default 4194303): +100M

Created a new partition 3 of type 'Linux' and of size 100 MiB.

Command (m for help): n
Partition type
   p   primary (3 primary, 0 extended, 1 free)
   e   extended (container for logical partitions)
Select (default e): p

Selected partition 4
First sector (616448-4194303, default 616448):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (616448-4194303, default 4194303): +100M

Created a new partition 4 of type 'Linux' and of size 100 MiB.
```

The `p` option was selected to ensure that the fourth partition was also created as a primary partition.

## 3. Verifying the New Partitions

Inside `fdisk`, the `p` command was used to display the updated partition table:

```text
Command (m for help): p
Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x9c63bfb2

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux
/dev/nvme1n1p3      411648 616447  204800  100M 83 Linux
/dev/nvme1n1p4      616448 821247  204800  100M 83 Linux
```

The four partitions on the secondary disk were organized as follows:

| Partition | Size | Purpose |
|---|---:|---|
| `/dev/nvme1n1p1` | 100 MiB | RAID 0 |
| `/dev/nvme1n1p2` | 100 MiB | RAID 0 |
| `/dev/nvme1n1p3` | 100 MiB | RAID 1 |
| `/dev/nvme1n1p4` | 100 MiB | RAID 1 |

The partition table was written using `w`, and the kernel was subsequently updated using `partprobe`:

```text
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

```bash
partprobe /dev/nvme1n1
```

## 4. Creating the RAID 1 Array

With the two new partitions available, the `/dev/md1` array was created using `mdadm`.

```bash
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/nvme1n1p3 /dev/nvme1n1p4
```

Complete output:

```text
┌──(root㉿kali)-[~]
└─# mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/nvme1n1p3 /dev/nvme1n1p4
To optimalize recovery speed, it is recommended to enable write-indent bitmap, do you want to enable it now? [y/N]? y
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
Continue creating array [y/N]? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md1 started.
```

The parameter:

```bash
--level=1
```

specifies RAID 1.

The parameter:

```bash
--raid-devices=2
```

indicates that the array consists of two devices.

`mdadm` also reported that the array would use version 1.2 metadata and confirmed that `/dev/md1` had started.

## 5. Verifying the RAID Device

The `ls -l` command was used to confirm that the `/dev/md1` device had been created:

```text
┌──(root㉿kali)-[~]
└─# ls -l /dev/md1
brw-rw---- 1 root disk 9, 1 out 6 16:53 /dev/md1
```

The presence of `/dev/md1` confirms that the RAID 1 device was made available by the system.

## 6. Checking the Array Status

The status of the RAID arrays present on the system was checked using `/proc/mdstat`:

```bash
cat /proc/mdstat
```

Output:

```text
┌──(root㉿kali)-[~]
└─# cat /proc/mdstat
Personalities : [raid0] [raid1] [raid6] [raid5] [raid4] [raid10] 
md1 : active raid1 nvme1n1p4[1] nvme1n1p3[0]
      101376 blocks super 1.2 [2/2] [UU]
      bitmap: 0/1 pages [0KB], 65536KB chunk

md0 : active raid0 nvme1n1p2[1] nvme1n1p1[0]
      200704 blocks super 1.2 512k chunks
      
unused devices: <none>
```

The output confirms that the new `md1` array is active as RAID 1:

```text
md1 : active raid1 nvme1n1p4[1] nvme1n1p3[0]
```

The indicator:

```text
[2/2] [UU]
```

shows that both expected devices are present and active in the array.

The previously created RAID 0 array (`md0`) is also still present:

```text
md0 : active raid0 nvme1n1p2[1] nvme1n1p1[0]
```

## 7. Formatting the RAID 1 Array

After creating and verifying the array, `/dev/md1` was formatted with the ext4 filesystem:

```bash
mkfs.ext4 /dev/md1
```

Output:

```text
┌──(root㉿kali)-[~]
└─# mkfs.ext4 /dev/md1
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 101376 1k blocks and 25376 inodes
Filesystem UUID: 11177e82-b1ac-4f49-9d22-8f5be016009b
Superblock backups stored on blocks: 
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

The ext4 filesystem was successfully created on the `/dev/md1` array.

## 8. Mounting the RAID 1 Array

The mount point was created:

```bash
mkdir /mnt/raid1
```

The array was then mounted:

```bash
mount /dev/md1 /mnt/raid1
```

To check the available space and confirm the mount, the following command was run:

```bash
df -h
```

Output:

```text
Sist. Arq.       Tam. Usado Disp. Uso% Montado em
udev             1,9G     0  1,9G   0% /dev
tmpfs            388M 1008K  387M   1% /run
/dev/nvme0n1p1    19G   18G  511M  98% /
tmpfs             1,9G     0  1,9G   0% /dev/shm
tmpfs             5,0M     0  5,0M   0% /run/lock
tmpfs             1,9G   556K  1,9G   1% /tmp
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-journald.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-udev-load-credentials.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-sysctl.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup-dev-early.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup-dev.service
/dev/nvme0n1p15  124M  286K  124M   1% /boot/efi
tmpfs             1,0M     0  1,9G   0% /run/credentials/serial-getty@ttyS0.service
tmpfs             388M   120K  388M   0% /run/user/0
tmpfs             388M   128K  388M   0% /run/user/1001
/dev/md0          179M    63K  165M   1% /mnt/raid0
/dev/md1           88M    46K   81M   1% /mnt/raid1
```

The final line confirms that the RAID 1 array is mounted:

```text
/dev/md1           88M    46K   81M   1% /mnt/raid1
```

The filesystem reports approximately 88 MiB of total space, with about 81 MiB available. Some capacity is used by the filesystem and its metadata.

With RAID 1, although two 100 MiB partitions are used, the usable capacity is based on only one member because the data is mirrored across both devices.

## Evidence

Evidence for this activity is included in the PDF for Module 7, Classes 25–26.

[View Evidence — Classes 25–26](../evidencias.pdf)

---

[Back to Classes 25–26](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
