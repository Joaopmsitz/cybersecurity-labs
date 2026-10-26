# Activity 7.10 — Overwriting with the DoD 5220.22-M Pattern

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 27–28  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Overwrite data on a partition using the `shred` command, applying one pass of random data followed by a pass of zeros.

This activity uses the DoD 5220.22-M standard as a reference, providing context for the data overwrite technique demonstrated in the lab.

## Environment

- **Operating system:** Kali Linux
- **Disk used:** `/dev/nvme1n1`
- **Existing partitions:** `/dev/nvme1n1p1` and `/dev/nvme1n1p2`
- **Tool:** `shred`
- **Partition used for overwriting:** `/dev/nvme1n1p2`

> The operation was performed only on the partition provided for the lab.

## 1. Switching to the Root User

Administrative access was obtained:

```bash
sudo -i
```

## 2. Checking the Disk

The `fdisk` utility was used to inspect the disk's partition table:

```bash
fdisk /dev/nvme1n1
```

Inside `fdisk`, the `p` command was used to display the partitions:

```text
Welcome to fdisk (util-linux 2.40.1).                                                            
Changes will remain in memory only, until you decide to write them.                              
Be careful before using the write command.

This disk is currently in use - repartitioning is probably a bad idea.
It's recommended to umount all file systems, and swapoff all swap partitions on this disk.

Command (m for help): p

Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store              
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x407f5a73

Device         Boot Start    End Sectors  Size Id Type
/dev/nvme1n1p1       2048 206847  204800  100M 83 Linux
```

The output shows that the existing `nvme1n1p1` partition occupies 100 MiB.

## 3. Creating the Second Partition

A new primary partition was created inside `fdisk`:

```text
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

The newly created partition was:

```text
/dev/nvme1n1p2
```

Its size was 100 MiB.

## 4. Writing the Partition Table

The changes were written using the `w` command:

```text
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

The kernel's partition table information was then updated:

```bash
partprobe /dev/nvme1n1
```

## 5. Verifying the Partitions

The device structure was checked using:

```bash
lsblk
```

Output:

```text
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
nvme1n1      259:0    0    2G  0 disk 
├─nvme1n1p2  259:5    0  100M  0 part 
└─nvme1n1p1  259:6    0  100M  0 part /home/aluno/Documentos/MeuHD
nvme0n1      259:1    0   20G  0 disk 
├─nvme0n1p1  259:2    0 19,9G  0 part /
├─nvme0n1p14 259:3    0    3M  0 part 
└─nvme0n1p15 259:4    0  124M  0 part /boot/efi
```

The output confirms the existence of the new partition:

```text
/dev/nvme1n1p2  100M
```

It will be used as the overwrite target.

## 6. Overwriting with Shred

The command specified in the lab was executed:

```bash
shred -vfz -n 1 /dev/nvme1n1p2
```

Output:

```text
shred: /dev/nvme1n1p2: passagem 1/2 (random)...
shred: /dev/nvme1n1p2: passagem 2/2 (000000)...
```

### Command Interpretation

The command used was:

```bash
shred -vfz -n 1 /dev/nvme1n1p2
```

Each option has a specific purpose:

- `-v` — displays detailed information during execution.
- `-f` — forces changes to file permissions when necessary.
- `-z` — performs a final pass that fills the device with zeros.
- `-n 1` — performs one overwrite pass using pseudorandom data.
- `/dev/nvme1n1p2` — the device to be overwritten.

The output shows the two passes performed:

```text
passagem 1/2 (random)
passagem 2/2 (000000)
```

Therefore, in this execution, `shred` performed one pass using random data and a second pass filling the target area with zeros.

## Technical Note on DoD 5220.22-M

The lab presents this technique in the context of the DoD 5220.22-M standard. However, the command executed:

```bash
shred -vfz -n 1 /dev/nvme1n1p2
```

should not be interpreted as a complete implementation of, or certification of compliance with, that standard.

With `-n 1` and `-z`, the operation consists of:

- One pass using pseudorandom data.
- One final pass using zeros.

The practical objective of the lab is to demonstrate the concept of data overwriting, making recovery of the previously stored content in the overwritten area more difficult.

Furthermore, overwriting techniques may have limitations on certain types of storage, especially SSDs and devices with internal block-management mechanisms.

## Evidence

The evidence requested for this activity corresponds to step 6, showing the execution of the `shred` command and the two passes performed.

Evidence for this activity is included in the PDF for Module 7, Classes 27–28.

[View Evidence — Classes 27–28](../evidencias.pdf)

---

[Back to Classes 27–28](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
