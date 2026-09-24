# Atividade 7.8 — Formatação Completa no Kali Linux

## Objetivo

Realizar o processo de preparação e formatação de uma partição no Kali Linux, removendo a configuração anterior de RAID, recriando o sistema de arquivos e, por fim, removendo as assinaturas do sistema de arquivos com `wipefs`.

O laboratório utiliza o disco `/dev/nvme1n1`, que não contém o sistema operacional principal da máquina virtual.

---

## Ambiente

* **Sistema:** Kali Linux
* **Disco utilizado:** `/dev/nvme1n1`
* **Partição trabalhada:** `/dev/nvme1n1p1`
* **Ferramentas:** `mdadm`, `fdisk`, `partprobe`, `mkfs.ext4` e `wipefs`

> As operações abaixo são destrutivas e foram realizadas somente no disco disponibilizado para o laboratório.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Identificação dos discos

Foi utilizado o comando `fdisk -l` para verificar os discos e partições disponíveis:

```bash
fdisk -l
```

Saída registrada no laboratório:

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

O disco utilizado no laboratório é o `/dev/nvme1n1`, enquanto o sistema operacional está instalado no `/dev/nvme0n1`.

---

## 3. Parada do dispositivo RAID

Como o disco secundário havia sido utilizado nas atividades anteriores para os arrays RAID, foi executado:

```bash
mdadm --stop /dev/nvme1n1
```

O objetivo dessa etapa é interromper a configuração RAID antes de realizar a limpeza e alteração das partições.

---

## 4. Remoção dos metadados RAID

Para remover as assinaturas de RAID das quatro partições existentes, foram executados:

```bash
mdadm --zero-superblock /dev/nvme1n1p1
mdadm --zero-superblock /dev/nvme1n1p2
mdadm --zero-superblock /dev/nvme1n1p3
mdadm --zero-superblock /dev/nvme1n1p4
```

O comando `mdadm --zero-superblock` remove os metadados de superbloco utilizados pelo RAID, permitindo que as partições deixem de ser identificadas como membros do array anterior.

---

## 5. Exclusão das partições antigas

Foi aberto o particionador do disco:

```bash
fdisk /dev/nvme1n1
```

As partições `p4`, `p3` e `p2` foram removidas, mantendo inicialmente a `p1`.

Saída registrada:

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

Depois das alterações, foi executado:

```bash
partprobe /dev/nvme1n1
```

O `partprobe` solicita ao kernel que releia a tabela de partições atualizada.

---

## 6. Formatação da partição

Com a partição `nvme1n1p1` disponível, foi criado um novo sistema de arquivos `ext4`:

```bash
mkfs.ext4 /dev/nvme1n1p1
```

Saída:

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

O comando `mkfs.ext4` criou uma nova estrutura de sistema de arquivos `ext4` na partição.

---

## 7. Remoção das assinaturas do sistema de arquivos

Após a formatação, foi utilizado o `wipefs` para remover as assinaturas reconhecidas do sistema de arquivos:

```bash
wipefs -a /dev/nvme1n1p1
```

Saída:

```text
/dev/nvme1n1p1: 2 bytes were erased at offset 0x00000438 (ext4): 53 ef
```

A saída indica que o `wipefs` identificou uma assinatura `ext4` no deslocamento `0x00000438` e removeu os dois bytes correspondentes (`53 ef`).

O parâmetro `-a` solicita a remoção de todas as assinaturas de sistemas de arquivos reconhecidas no dispositivo.

> **Observação:** `wipefs -a` remove assinaturas e metadados identificadores do sistema de arquivos. Ele não deve ser interpretado como uma técnica de apagamento seguro de todos os dados existentes no dispositivo.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 7**, registrando a execução do comando `wipefs` e a remoção da assinatura `ext4`.

[**Evidências — Módulo 7 / Aulas 27 e 28**](../evidencias.pdf)
