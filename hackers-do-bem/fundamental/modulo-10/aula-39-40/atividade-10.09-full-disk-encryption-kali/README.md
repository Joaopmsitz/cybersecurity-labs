# Activity 10.09 — Full Disk Encryption on a Partition in Kali Linux

## Objective

Implement partition encryption on Kali Linux using **LUKS (Linux Unified Key Setup)** by creating a dedicated partition, protecting it with a password, formatting it with ext4, and mounting and unmounting it.

> Although the lab uses the term **Full Disk Encryption (FDE)**, this activity specifically encrypts the partition `/dev/nvme1n1p3`, not the entire disk.

---

## Environment

- **Operating system:** Kali GNU/Linux Rolling
- **Access:** RDP
- **Main disk:** `/dev/nvme0n1`
- **Disk used in the activity:** `/dev/nvme1n1`
- **Created partition:** `/dev/nvme1n1p3`
- **New partition size:** 200 MiB
- **Encryption technology:** LUKS
- **Filesystem:** ext4
- **Cryptographic mapping:** `Teste`
- **Mount point:** `/mnt/encrypted`

---

## 1. Accessing Kali Linux

The Kali Linux machine was started and accessed remotely.

After connecting, a terminal was opened and administrative privileges were obtained:

```bash
sudo -i
```

---

## 2. Identifying Disks and Partitions

The following command was used:

```bash
fdisk -l
```

The output showed two disks. The main disk was `/dev/nvme0n1`, while the disk used in this activity was `/dev/nvme1n1`.

The output for the disk used in the activity was:

```text
Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/O size (minimum/optimal): 4096 bytes
Disklabel type: dos
Disk identifier: 0xf8a2dbef

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux
```

The `/dev/nvme1n1` disk had available space for creating a new partition.

---

## 3. Accessing the Disk with fdisk

The following command was used:

```bash
fdisk /dev/nvme1n1
```

Inside `fdisk`, the `p` command was used to display the partition table:

```text
Welcome to fdisk (util-linux 2.41.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): p
Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xf8a2dbef

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux
```

---

## 4. Creating a New Partition

The `n` option was used to create a new primary partition.

The following settings were used:

- **Partition number:** `3`
- **First sector:** Default
- **Last sector:** `+200M`
- **Type:** Linux

The resulting output was:

```text
Command (m for help): n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (3,4, default 3):
First sector (411648-4194303, default 411648):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (411648-4194303, default 4194303): +200M

Created a new partition 3 of type 'Linux' and of size 200 MiB.
```

The newly created partition was:

```text
/dev/nvme1n1p3
```

Its size was approximately **200 MiB**.

---

## 5. Verifying and Writing the Partition Table

The `p` command was used again to verify the configuration:

```text
Command (m for help): p
Disk /dev/nvme1n1: 2 GiB, 2147483648 bytes, 4194304 sectors
Disk model: Amazon Elastic Block Store
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x407f5a73

Device         Boot  Start    End Sectors  Size Id Type
/dev/nvme1n1p1        2048 206847  204800  100M 83 Linux
/dev/nvme1n1p2      206848 411647  204800  100M 83 Linux
/dev/nvme1n1p3      411648 821247  409600  200M 83 Linux

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

After exiting `fdisk`, the following command was executed:

```bash
partprobe /dev/nvme1n1
```

The `partprobe` command asks the system to reread the partition table, allowing the new partition to be recognized without restarting the machine.

---

## 6. Initializing LUKS Encryption

The newly created partition was configured to use LUKS with the following command:

```bash
cryptsetup luksFormat /dev/nvme1n1p3
```

`cryptsetup` displayed a warning that the operation would permanently overwrite existing data on the partition.

```text
WARNING!
========
This will overwrite data on /dev/nvme1n1p3 permanently.

Are you sure? (Type 'yes' in capital letters): YES
Enter passphrase for /dev/nvme1n1p3:
Verify passphrase:
```

A password was set to protect the encrypted volume.

> The password used in the lab is not recorded in this README.

---

## 7. Opening the Encrypted Volume

After initializing LUKS, the partition was opened using:

```bash
cryptsetup luksOpen /dev/nvme1n1p3 Teste
```

The name `Teste` was used as the identifier for the encrypted device mapping.

The volume then became accessible through:

```text
/dev/mapper/Teste
```

---

## 8. Creating the ext4 Filesystem

The encrypted volume was formatted with ext4:

```bash
mkfs.ext4 /dev/mapper/Teste
```

The resulting output was:

```text
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 188416 1k blocks and 47104 inodes
Filesystem UUID: 5a8348f9-b7d0-4cf6-8d4d-7dd8e59fe7f0
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information:
done
```

At this stage, the ext4 filesystem was created on the device mapped by LUKS.

---

## 9. Creating the Mount Point

The directory used to access the volume was created with:

```bash
mkdir -m 777 /mnt/encrypted
```

The `-m 777` option set the directory permissions according to the procedure specified by the lab.

**Security note:** Permissions of `777` allow all local users to read, write, and access the directory. This is generally not recommended for sensitive data in a production environment.

---

## 10. Mounting the Encrypted Volume

The volume was mounted using:

```bash
mount /dev/mapper/Teste /mnt/encrypted
```

The contents of the encrypted filesystem then became accessible through:

```text
/mnt/encrypted
```

---

## 11. Unmounting the Volume

After the volume was used, it was unmounted with:

```bash
umount /mnt/encrypted
```

This step ends access to the filesystem through the mount point. The LUKS mapping remains open until it is explicitly closed.

---

## 12. Verifying the Volume in the Graphical Environment

After unmounting, the following drive label was observed on the desktop:

```text
Volume de 193MB
```

The volume was accessed through the graphical environment by opening its corresponding icon and viewing the folder in **Thunar**.

### Evidence — Step 12

**Caption to include before the screenshot:**

> Screenshot of Activity 10.09: the encrypted volume labeled `Volume de 193MB` displayed on the Kali Linux desktop and accessed through the Thunar file manager.

[View Evidence — Classes 39–40](../evidencias.pdf)

After capturing the evidence, Thunar and the terminal were closed.

---

## Key Concepts

- **LUKS:** A standard used on Linux to implement encryption for block devices.
- **cryptsetup:** A utility used to configure and open LUKS volumes.
- **`/dev/mapper/Teste`:** The logical device made available after opening the encrypted volume.
- **ext4:** The filesystem created on top of the encrypted volume.
- **`mount` / `umount`:** Commands used to mount and unmount a filesystem.

## Activity Workflow

```text
Identify the disk
      ↓
Create /dev/nvme1n1p3
      ↓
Configure LUKS
      ↓
Open the encrypted volume
      ↓
Create the ext4 filesystem
      ↓
Mount at /mnt/encrypted
      ↓
Unmount the filesystem
      ↓
Verify the volume in Thunar
```

## Result

The `/dev/nvme1n1p3` partition was created, configured with **LUKS**, opened using `cryptsetup`, and formatted with **ext4**. The volume was mounted, unmounted, and subsequently identified in the Kali Linux graphical environment.

---

[Back to Classes 39–40](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
