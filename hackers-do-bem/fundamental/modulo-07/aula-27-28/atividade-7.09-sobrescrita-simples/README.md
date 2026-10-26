# Activity 7.09 — Simple Overwrite on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 27–28  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Perform a simple overwrite on a partition in Kali Linux using random data, writing to the device until no space is available.

This activity demonstrates a low-level data overwrite technique using the `dd` command and allows observation of the filesystem's state after the operation.

## Environment

- **Operating system:** Kali Linux
- **Disk used:** `/dev/nvme1n1`
- **Partition used:** `/dev/nvme1n1p1`
- **Filesystem:** ext4
- **Tools:** `mkfs.ext4`, `mount`, `dd`, and `df`

> The overwrite operation was performed only on the partition provided for the lab. Writing directly to a block device is destructive and can destroy filesystem metadata and make existing data inaccessible.

## 1. Switching to the Root User

Administrative access was obtained:

```bash
sudo -i
```

## 2. Formatting and Mounting the Partition

The partition used in the previous activity was formatted again with ext4:

```bash
mkfs.ext4 /dev/nvme1n1p1
```

Output:

```text
mke2fs 1.47.2 (1-Jan-2025)
Creating filesystem with 102400 1k blocks and 25584 inodes
Filesystem UUID: 9623bee1-0ab5-41cb-8a04-56c8a19893e6
Superblock backups stored on blocks: 
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

Next, the directory used as the mount point was created:

```bash
mkdir -m 777 /home/aluno/Documentos/MeuHD
mount /dev/nvme1n1p1 /home/aluno/Documentos/MeuHD
```

The partition then became accessible through the following directory:

```text
/home/aluno/Documentos/MeuHD
```

## 3. Creating the Test File

The mount point was accessed:

```bash
cd /home/aluno/Documentos/MeuHD
```

The following file was then created:

```bash
nano Teste.txt
```

Content entered:

```text
Teste
```

Before the overwrite, the directory contents were checked:

```bash
ls
```

Output:

```text
lost+found  Teste.txt
```

The `Teste.txt` file represents data that existed on the partition before the overwrite operation.

## 4. Overwriting with Random Data

The following command was used to fill the partition with data from `/dev/urandom`:

```bash
dd if=/dev/urandom of=/dev/nvme1n1p1 bs=10M
```

Output:

```text
dd: erro de escrita de '/dev/nvme1n1p1': Não há espaço disponível no dispositivo
11+0 records in
10+0 records out
104857600 bytes (105 MB, 100 MiB) copied, 0,938747 s, 112 MB/s
```

### Interpretation

The command used was:

```bash
dd if=/dev/urandom of=/dev/nvme1n1p1 bs=10M
```

Each parameter has a specific purpose:

- `dd` — performs low-level data copying.
- `if=/dev/urandom` — specifies `/dev/urandom` as the source of random data.
- `of=/dev/nvme1n1p1` — specifies the partition as the destination.
- `bs=10M` — uses 10 MiB blocks for each operation.

Execution continued until the device could no longer accept additional data:

```text
dd: erro de escrita de '/dev/nvme1n1p1': Não há espaço disponível no dispositivo
```

The output also indicates:

```text
10+0 records out
104857600 bytes (105 MB, 100 MiB) copied
```

In other words, 10 blocks of 10 MiB were successfully written, totaling 100 MiB.

The final error occurred because the command attempted to continue writing after the available space on the partition had been exhausted.

## 5. Checking Space Usage

After the overwrite, the following command was executed:

```bash
df -h
```

Output recorded during the lab:

```text
Sist. Arq.       Tam. Usado Disp. Uso% Montado em
udev             1,9G     0  1,9G   0% /dev
tmpfs            388M  964K  387M   1% /run
/dev/nvme0n1p1    20G   12G  6,9G  64% /
tmpfs            1,9G     0  1,9G   0% /dev/shm
tmpfs            5,0M     0  5,0M   0% /run/lock
tmpfs            1,9G     0  1,9G   0% /tmp
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-journald.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-udev-load-credentials.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-udev-load-credentials.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-sysctl.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-tmpfiles-setup-dev-early.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-tmpfiles-setup-dev.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-tmpfiles-setup.service
tmpfs            1,0M     0  1,0M   0% /run/credentials/getty@tty1.service
tmpfs            388M  120K  388M   1% /run/user/0
tmpfs            388M  128K  388M   1% /run/user/1001
/dev/nvme1n1p1   948G  948G     0 100% /home/aluno/Documentos/MeuHD
```

The recorded output shows the `/dev/nvme1n1p1` partition with the following values:

```text
948G  948G     0 100%
```

According to the output recorded during the lab, the device was completely full.

> **Note:** The capacity values above have been preserved as recorded during the lab, even though they appear inconsistent with the approximately 100 MiB partition size reported earlier.

## 6. System Behavior After the Overwrite

After the partition had been filled, attempting to list its contents again produced the following message in the lab environment:

```text
ls: lendo o diretório '.': A estrutura necessita de limpeza
```

This indicates that the direct write to the device altered structures that previously belonged to the filesystem.

The operation was performed directly on:

```text
/dev/nvme1n1p1
```

It was not performed through an ordinary file within the mounted filesystem.

## Evidence

The evidence requested for this activity corresponds to step 7, showing the output of `df -h` after the overwrite.

Evidence for this activity is included in the PDF for Module 7, Classes 27–28.

[View Evidence — Classes 27–28](../evidencias.pdf)

---

[Back to Classes 27–28](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
