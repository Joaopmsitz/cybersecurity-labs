# Atividade 7.2 — Aplicando o Software RAID 1 no Kali Linux

## Objetivo

Implementar um **Software RAID 1** no Kali Linux utilizando duas novas partições de 100 MiB no disco secundário `/dev/nvme1n1`.

O RAID 1 utiliza **espelhamento (mirroring)**, mantendo uma cópia dos dados em cada dispositivo que compõe o array. Neste laboratório, o array será criado com o `mdadm`, formatado com `ext4` e montado em `/mnt/raid1`.

A atividade aproveita o mesmo disco secundário utilizado anteriormente no RAID 0, criando as partições `/dev/nvme1n1p3` e `/dev/nvme1n1p4`.

---

## 1. Verificação dos discos e arrays existentes

Inicialmente, foi utilizado o comando `fdisk -l` para verificar a configuração atual dos discos e dos arrays criados anteriormente.

```text id="c9w2km"
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

O disco `/dev/nvme1n1` já possuía as duas partições de 100 MiB utilizadas na atividade anterior:

* `/dev/nvme1n1p1`
* `/dev/nvme1n1p2`

Também estava presente o array `/dev/md0`, correspondente ao RAID 0 criado anteriormente.

As novas partições para o RAID 1 serão criadas a partir do espaço disponível após `/dev/nvme1n1p2`.

---

## 2. Criação das partições do RAID 1

Foi utilizado o `fdisk` no disco secundário:

```bash id="n7k1ve"
fdisk /dev/nvme1n1
```

Foram criadas duas novas partições primárias de 100 MiB cada:

* `/dev/nvme1n1p3`
* `/dev/nvme1n1p4`

Saída do procedimento:

```text id="a8x3qp"
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

A opção `p` foi utilizada para garantir que a quarta partição também fosse criada como uma partição primária.

---

## 3. Verificação das novas partições

Dentro do `fdisk`, foi utilizado o comando `p` para visualizar a tabela atualizada:

```text id="q2v6rt"
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

As quatro partições do disco secundário ficaram organizadas da seguinte forma:

| Partição         | Tamanho | Utilização |
| ---------------- | ------: | ---------- |
| `/dev/nvme1n1p1` | 100 MiB | RAID 0     |
| `/dev/nvme1n1p2` | 100 MiB | RAID 0     |
| `/dev/nvme1n1p3` | 100 MiB | RAID 1     |
| `/dev/nvme1n1p4` | 100 MiB | RAID 1     |

A tabela foi gravada com `w` e, posteriormente, o kernel foi atualizado com `partprobe`:

```text id="z7j4mx"
Command (m for help): w
The partition table has been altered.
Syncing disks.

┌──(root㉿kali)-[~]
└─# partprobe /dev/nvme1n1
```

---

## 4. Criação do RAID 1

Com as duas novas partições disponíveis, foi criado o array `/dev/md1` utilizando o `mdadm`.

```bash id="k4t8pw"
mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/nvme1n1p3 /dev/nvme1n1p4
```

Saída completa:

```text id="r6c1za"
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

O parâmetro:

```text
--level=1
```

define o RAID 1.

Já:

```text
--raid-devices=2
```

indica que o array será composto por dois dispositivos.

O `mdadm` também informou que o array utilizaria metadata versão 1.2 e iniciou o dispositivo `/dev/md1`.

---

## 5. Verificação do dispositivo RAID

Foi utilizado `ls -l` para confirmar que o dispositivo `/dev/md1` foi criado:

```text id="m5h2yv"
┌──(root㉿kali)-[~]
└─# ls -l /dev/md1
brw-rw---- 1 root disk 9, 1 out 6 16:53 /dev/md1
```

A presença de `/dev/md1` confirma que o dispositivo RAID 1 foi disponibilizado pelo sistema.

---

## 6. Verificação do estado dos arrays

O estado dos arrays RAID presentes no sistema foi consultado através do arquivo `/proc/mdstat`:

```bash id="c3q8nf"
cat /proc/mdstat
```

Saída:

```text id="v1m7ks"
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

A saída confirma que o novo array `md1` está ativo como **RAID 1**:

```text
md1 : active raid1 nvme1n1p4[1] nvme1n1p3[0]
```

A indicação:

```text
[2/2] [UU]
```

mostra que os dois dispositivos esperados estão presentes e ativos no array.

Também é possível observar que o RAID 0 anterior (`md0`) continua presente:

```text
md0 : active raid0 nvme1n1p2[1] nvme1n1p1[0]
```

---

## 7. Formatação do RAID 1

Após a criação e verificação do array, o `/dev/md1` foi formatado utilizando `ext4`:

```bash id="w3j9qb"
mkfs.ext4 /dev/md1
```

Saída:

```text id="p8s4kd"
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

O sistema de arquivos `ext4` foi criado com sucesso no array `/dev/md1`.

---

## 8. Montagem do RAID 1

Foi criado o ponto de montagem:

```bash id="z8v5nc"
mkdir /mnt/raid1
```

Em seguida, o array foi montado:

```bash id="q9r2ls"
mount /dev/md1 /mnt/raid1
```

Para verificar o espaço disponível e confirmar a montagem, foi executado:

```bash id="u6c4xf"
df -h
```

Resultado:

```text id="d2k8wv"
┌──(root㉿kali)-[~]
└─# df -h
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
tmpfs             388M   120K  388M   1% /run/user/0
tmpfs             388M   128K  388M   0% /run/user/1001
/dev/md0          179M    63K  165M   1% /mnt/raid0
/dev/md1           88M    46K   81M   1% /mnt/raid1
```

A última linha confirma a montagem do RAID 1:

```text
/dev/md1           88M    46K   81M   1% /mnt/raid1
```

O espaço disponível ficou em aproximadamente **88 MiB**, com cerca de **81 MiB livres**, devido ao espaço utilizado pelo sistema de arquivos e seus metadados.

No RAID 1, embora duas partições de 100 MiB sejam utilizadas, a capacidade útil é baseada em apenas um dos dispositivos, pois os dados são espelhados entre eles.

---

## Evidência

[**Evidências — Módulo 7 / Aulas 1 e 2**](../evidencias.pdf)
