# Atividade 7.1 — Aplicando o Software RAID 0 no Kali Linux

## Objetivo

Implementar um **Software RAID 0** no Kali Linux utilizando duas partições de 100 MiB criadas em um segundo disco da máquina virtual.

O RAID 0 utiliza **striping**, distribuindo os dados entre os dispositivos que compõem o array. Neste laboratório, o array será criado com o utilitário `mdadm`, formatado com `ext4` e montado em `/mnt/raid0`.

> **Observação:** o laboratório utiliza o disco secundário `/dev/nvme1n1`. O disco principal `/dev/nvme0n1` não deve ser utilizado para a criação do RAID.

---

## 1. Identificação dos discos

Inicialmente, foi utilizado o comando `fdisk -l` para verificar os discos disponíveis na máquina virtual.

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

O disco utilizado para o laboratório foi o `/dev/nvme1n1`, um segundo volume EBS de 2 GiB anexado à máquina virtual.

O `/dev/nvme0n1` contém o sistema operacional e suas partições, enquanto o `/dev/nvme1n1` foi utilizado exclusivamente para os testes do RAID.

---

## 2. Criação das partições para o RAID 0

Foi utilizado o `fdisk` no disco `/dev/nvme1n1`:

```bash
fdisk /dev/nvme1n1
```

Foram criadas duas partições primárias de 100 MiB cada, utilizando os valores padrão nos campos em que somente `Enter` era solicitado.

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

Após a criação, foi utilizado `p` dentro do `fdisk` para conferir a tabela de partições:

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

As duas partições utilizadas pelo RAID 0 ficaram, portanto:

* `/dev/nvme1n1p1` — 100 MiB
* `/dev/nvme1n1p2` — 100 MiB

Para gravar a nova tabela de partições, foi utilizado `w`:

```text
Command (m for help): w
The partition table has been altered.
Syncing disks.

┌──(root㉿kali)-[~]
└─# partprobe /dev/nvme1n1
```

O `partprobe` faz com que o kernel reconheça a alteração na tabela de partições sem precisar reiniciar a máquina.

---

## 3. Criação do RAID 0 com mdadm

Com as duas partições disponíveis, foi criado o array `/dev/md0` utilizando o `mdadm`.

```bash
mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme1n1p1 /dev/nvme1n1p2
```

Saída:

```text
┌──(root㉿kali)-[~]
└─# mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/nvme1n1p1 /dev/nvme1n1p2
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```

O parâmetro `--level=0` define o nível RAID utilizado, enquanto `--raid-devices=2` informa que o array será composto por dois dispositivos.

O array criado recebeu o nome `/dev/md0`.

---

## 4. Verificação do dispositivo RAID

Foi utilizado `ls -l` para confirmar a criação do dispositivo:

```text
┌──(root㉿kali)-[~]
└─# ls -l /dev/md0
brw-rw---- 1 root disk 9, 0 fev 18 12:04 /dev/md0
```

A presença de `/dev/md0` confirma que o dispositivo RAID foi criado pelo sistema.

---

## 5. Formatação do RAID 0

O dispositivo `/dev/md0` foi formatado utilizando o sistema de arquivos `ext4`:

```bash
mkfs.ext4 /dev/md0
```

Saída:

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

A saída mostra que o sistema de arquivos `ext4` foi criado com sucesso no array `/dev/md0`.

---

## 6. Montagem do RAID 0

Foi criado o diretório `/mnt/raid0` para servir como ponto de montagem:

```bash
mkdir /mnt/raid0
```

Em seguida, o dispositivo RAID foi montado:

```bash
mount /dev/md0 /mnt/raid0
```

Para verificar o espaço disponível e confirmar a montagem, foi executado:

```bash
df -h
```

Resultado:

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
/dev/nvme0n1p15  124M  286K  124M   1% /boot/efi
tmpfs             1,0M     0  1,9G   0% /run/credentials/systemd-tmpfiles-setup.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/serial-getty@ttyS0.service
tmpfs             1,0M     0  1,9G   0% /run/credentials/getty@tty1.service
tmpfs             388M   120K  388M   1% /run/user/0
tmpfs             388M   128K  388M   0% /run/user/1001
/dev/md0          179M    63K  165M   1% /mnt/raid0
```

A última linha confirma que o `/dev/md0` está montado em `/mnt/raid0`.

O espaço disponível ficou em aproximadamente **179 MiB**, com cerca de **165 MiB livres**, devido ao espaço utilizado pelo sistema de arquivos e seus metadados.

---

## 7. Verificação final da configuração

Por fim, foi executado novamente o `fdisk -l` para visualizar as partições utilizadas e o dispositivo RAID criado.

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
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 524288 bytes / 1048576 bytes
```

O resultado final mostra:

* `/dev/nvme1n1p1` — 100 MiB
* `/dev/nvme1n1p2` — 100 MiB
* `/dev/md0` — array RAID 0 criado a partir das duas partições
* Sistema de arquivos `ext4`
* Ponto de montagem: `/mnt/raid0`

## Evidência

[**Evidências — Módulo 7 / Aulas 1 e 2**](../evidencias.pdf)
