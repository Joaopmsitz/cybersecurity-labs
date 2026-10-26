# Activity 12.10 — Acquiring a Disk Image on Kali Linux

In this activity, a partition was acquired using the `dd` command, creating a block-level copy of partition `/dev/nvme1n1p3` in a file.

> **Note:** Credentials used in the lab environment are not recorded in this document.

## Objective

- Identify available disk partitions.
- Use `dd` to perform a block-level copy.
- Create a partition image in a file.
- Verify the size and attributes of the acquired file.

## Procedure

### 1. Accessing Kali Linux

Kali Linux was accessed via RDP using the address `192.168.98.40`.

Administrative privileges were obtained using:

```bash
sudo -i
```

### 2. Identifying Partitions

The following command was executed:

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

The partition selected for acquisition was:

```text
/dev/nvme1n1p3
```

### 3. Acquiring the Partition

The `dd` command was used to copy the partition's contents into a file:

```bash
dd if=/dev/nvme1n1p3 of=/home/aluno/Documentos/Arquivos/Backup_nvme1n1p3
```

Output:

```text
409600+0 registos entrados
409600+0 registos saídos
209715200 bytes (210 MB, 200 MiB) copiados, 1,58606 s, 132 MB/s
```

The main parameters used were:

- **`dd`:** A tool for performing block-level copy operations.
- **`if=/dev/nvme1n1p3`:** The input device, corresponding to the partition being examined.
- **`of=/home/aluno/Documentos/Arquivos/Backup_nvme1n1p3`:** The output file that received the copy.

The result indicates that 209715200 bytes were processed, equivalent to approximately 200 MiB, at an average transfer rate of 132 MB/s.

### 4. Verifying the File

The destination directory was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The following command was then executed:

```bash
ls
```

Output:

```text
Backup_nvme1n1p3
```

### 5. Analyzing the File Attributes

The `stat` command was used:

```bash
stat Backup_nvme1n1p3
```

Output:

```text
Arquivo: Backup_nvme1n1p3
Tamanho: 209715200  Blocos: 409608     bloco de E/S: 4096   regular file
Dispositivo: 259,1      Inode: 540401      Ligações: 1
     Acesso: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
     Acesso: 2025-12-06 20:21:39.792758433 -0300
Modificação: 2025-12-06 20:21:41.364764169 -0300
  Alteração: 2025-12-06 20:21:41.364764169 -0300
    Criação: 2025-12-06 20:21:39.792758433 -0300
```

The output provides information about the image size, number of blocks, inode, permissions, owner, and timestamps of the created file.

### 6. Removing the Image

After verification, the acquired file was removed:

```bash
rm Backup_nvme1n1p3
```

The directory was checked again:

```bash
ls
```

The backup file was no longer present.

## Key Concepts

- **Image acquisition:** Creating a copy of data from storage media or a partition for analysis.
- **`dd`:** Performs block-level copying.
- **`if`:** Specifies the source of the data.
- **`of`:** Specifies the destination.
- **`stat`:** Displays file attributes and timestamps.
- **Forensic image:** Can be used as a source for analysis without working directly on the original media.

## Activity Workflow

```text
Partition
   ↓
fdisk -l
   ↓
/dev/nvme1n1p3
   ↓
dd
   ↓
Backup_nvme1n1p3
   ↓
stat
   ↓
Verify the acquisition
   ↓
Remove the file
```

## Result

A block-level copy of partition `/dev/nvme1n1p3` was created, producing a file containing 209715200 bytes. The file was subsequently examined using `stat` and removed at the end of the activity.

## Evidence

**View Evidence — Module 12 / Classes 47–48**

**Required screenshot:** Step 5 — output of the `stat Backup_nvme1n1p3` command.

---

[Back to Classes 47–48](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
