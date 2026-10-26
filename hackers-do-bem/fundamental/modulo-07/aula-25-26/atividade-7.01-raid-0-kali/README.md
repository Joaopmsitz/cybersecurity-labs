# Activity 7.01 — Implementing Software RAID 0 on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Class:** 25–26  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Implement a software RAID 0 array on Kali Linux using two 100 MiB partitions created on a secondary disk attached to the virtual machine.

RAID 0 uses **striping**, distributing data across the devices that make up the array. In this laboratory, the array was created using `mdadm`, formatted with the ext4 filesystem, and mounted at `/mnt/raid0`.

**Important:** The laboratory uses the secondary disk `/dev/nvme1n1`. The primary disk `/dev/nvme0n1` must not be used to create the RAID array.

RAID 0 improves aggregate storage performance in some workloads but provides no redundancy. If either member fails, the entire array may become unavailable and its data may be lost.

## 1. Identify the Disks

Initially, the `fdisk -l` command was used to inspect the disks available in the virtual machine.

```text
┌──(root㉿kali)-[~]
└─# fdisk -l
Disk /dev/nvme0n1: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: gpt
Disk identifier: 9FFA977A-4F2F-44A0-BCAC-15A77352798A

Device           Start      End  Sectors  Size Type
/dev/nvme0n1p1  262144 41943006 41680863 19,9G Linux filesystem
/dev/nvme0n1p14   2048     8191     6144    3M BIOS boot
/dev/nvme0n1p15   8192   262143   253952  124M EFI System

Partition table entries are not in disk order.


Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
```

The disk used for the laboratory was `/dev/nvme1n1`, a secondary 2 GiB EBS volume attached to the virtual machine.

The `/dev/nvme0n1` disk contains the operating system and its partitions, while `/dev/nvme1n1` was used exclusively for the RAID tests.

## 2. Create the Partitions for RAID 0

The `fdisk` utility was used on `/dev/nvme1n1`:

```bash
fdisk /dev/nvme1n1
```

Two primary partitions of 100 MiB each were created, accepting the default values whenever only Enter was requested.

```text
┌──(root㉿kali)-[~]
└─# fdisk /dev/nvme1n1

Welcome to fdisk (util-linux 2.41.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

This disk is currently in use - repartitioning is probably a bad idea.
It's recommended to umount all file systems, and swapoff all swap
partitions on this disk.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (1-4, default 1):
First sector (2048-4194303, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-4194303, default 4194303): +100M

Created a new partition 1 of type 'Linux' and of size 100 MiB.

Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (2-4, default 2):
First sector (206848-4194303, default 206848):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (206848-4194303, default 4194303): +100M

Created a new partition 2 of type 'Linux' and of size 100 MiB.
```

After creating the partitions, the `p` command was entered in `fdisk` to inspect the partition table:

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
```

The two partitions used by RAID 0 were therefore:

- `/dev/nvme1n1p1` — 100 MiB
- `/dev/nvme1n1p2` — 100 MiB

The `w` command was used to write the new partition table:

```text
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

The following command was then executed:

```bash
partprobe /dev/nvme1n1
```

`partprobe` asks the kernel to recognize changes to the partition table without requiring a system reboot.

## 3. Create the RAID 0 Array with `mdadm`

With both partitions available, the `/dev/md0` array was created using `mdadm`.

```bash
mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme1n1p1 /dev/nvme1n1p2
```

**Output:**

```text
┌──(root㉿kali)-[~]
└─# mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme1n1p1 /dev/nvme1n1p2
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```

The `--level=0` parameter defines the RAID level, while `--raid-devices=2` specifies that the array consists of two devices.

The resulting array was named `/dev/md0`.

## 4. Verify the RAID Device

The `ls -l` command was used to confirm that the device had been created:

```text
┌──(root㉿kali)-[~]
└─# ls -l /dev/md0
brw-rw---- 1 root disk 9, 0 fev 18 12:04 /dev/md0
```

The presence of `/dev/md0` confirms that the RAID device was created by the system.

## 5. Format the RAID 0 Array

The `/dev/md0` device was formatted with the ext4 filesystem:

```bash
mkfs.ext4 /dev/md0
```

**Output:**

```text
┌──(root㉿kali)-[~]
└─# mkfs.ext4 /dev/md0
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 200704 1k blocks and 50200 inodes
Filesystem UUID: 2af2ba0a-a2bc-4054-bce9-76b569b15ede
Superblock backups stored on blocks: 
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

The output shows that the ext4 filesystem was successfully created on the `/dev/md0` array.

## 6. Mount the RAID 0 Array

The `/mnt/raid0` directory was created as the mount point:

```bash
mkdir /mnt/raid0
```

The RAID device was then mounted:

```bash
mount /dev/md0 /mnt/raid0
```

To check the available space and confirm the mount, the following command was executed:

```bash
df -h
```

**Result:**

```text
┌──(root㉿kali)-[~]
└─# df -h
Sist. Arq.       Tam. Usado Disp. Uso% Montado em
udev             1,9G     0  1,9G   0% /dev
tmpfs            388M     0  388M   0% /run
/dev/nvme0n1p1    19G   18G  511M  98% /
tmpfs             1,9G     0  1,9G   0% /dev/shm
tmpfs             5,0M     0  5,0M   0% /run/lock
tmpfs             1,9G   424K  1,9G   1% /tmp
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-journald.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-udev-load-credentials.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-sysctl.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup-dev-early.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup-dev.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/serial-getty@ttyS0.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/getty@tty1.service
tmpfs             388M   120K  388M   1% /run/user/0
tmpfs             388M   128K  388M   0% /run/user/1001
/dev/md0          179M    63K  165M   1% /mnt/raid0
```

The last line confirms that `/dev/md0` is mounted at `/mnt/raid0`.

The filesystem reports approximately 179 MiB of total space, with about 165 MiB available. Some capacity is used by the filesystem and its metadata.

## 7. Verify the Final Configuration

Finally, `fdisk -l` was executed again to inspect the partitions used and the created RAID device.

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
Units: sectors of 1 * 512 bytes, 4096 bytes
I/O size (minimum/optimal): 524288 bytes / 1048576 bytes
```

The final output shows:

- `/dev/nvme1n1p1` — 100 MiB
- `/dev/nvme1n1p2` — 100 MiB
- `/dev/md0` — RAID 0 array created from the two partitions
- **Filesystem:** ext4
- **Mount point:** `/mnt/raid0`

The reported array capacity is approximately 196 MiB, while the mounted ext4 filesystem reports about 179 MiB. The difference reflects filesystem formatting overhead and the way the tools report available capacity.

## Results

The activity demonstrated how to create a software RAID 0 array on Kali Linux using two partitions on a secondary disk.

The process included:

1. Identifying the available disks.
2. Creating two 100 MiB partitions on `/dev/nvme1n1`.
3. Creating the RAID 0 array `/dev/md0` with `mdadm`.
4. Verifying the RAID device.
5. Formatting the array with ext4.
6. Mounting it at `/mnt/raid0`.
7. Verifying the final device and partition configuration.

The resulting array was successfully created and mounted.

**Security and availability note:** RAID 0 provides no fault tolerance or redundancy. Because data is striped across both partitions, the failure of either member can make the entire array inaccessible. RAID 0 should not be used as a substitute for backups or redundancy when data availability matters.

## Evidence

The activity evidence is included in the PDF for Module 07, Classes 25–26.

[View Evidence — Classes 25–26](../evidencias.pdf)

---

[Back to Classes 25–26](../) · [Back to Module 07](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
