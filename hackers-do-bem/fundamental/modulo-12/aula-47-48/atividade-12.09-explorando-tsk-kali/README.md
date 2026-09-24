# Atividade 12.9 — Explorando The Sleuth Kit (TSK) no Kali Linux

Nesta atividade foi realizada uma introdução ao **The Sleuth Kit (TSK)** no Kali Linux, utilizando comandos de análise forense para examinar uma partição e seus inodes.

> **Observação:** credenciais utilizadas no ambiente de laboratório não são registradas neste documento.

## Objetivo

* Identificar partições disponíveis no sistema.
* Utilizar ferramentas do The Sleuth Kit.
* Listar arquivos e diretórios de uma partição.
* Consultar informações relacionadas a inodes e seus timestamps.

## Procedimento

### 1. Acesso ao Kali Linux

O Kali Linux foi acessado via RDP pelo endereço `192.168.98.40`.

Foi obtido acesso administrativo:

```bash
sudo -i
```

### 2. Identificação dos discos e partições

Foi utilizado:

```bash
fdisk -l
```

Saída:

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

A partição principal utilizada pelo sistema é:

```text
/dev/nvme0n1p1
```

### 3. Conceito de inode

No Linux, um **inode** é uma estrutura utilizada pelo sistema de arquivos para armazenar informações sobre um arquivo ou diretório, como identificador, permissões, proprietário, tamanho e timestamps.

Em análise forense, informações de inode podem auxiliar na reconstrução de eventos relacionados aos arquivos.

### 4. Listagem com `fls`

Foi utilizado o comando:

```bash
fls /dev/nvme0n1p1
```

Saída:

```text
d/d 524461:     home
d/d 11:         lost+found
d/d 131073:     boot
d/d 396737:     curso
d/d 524289:     var
d/d 393229:     etc
d/d 131075:     usr
l/l 13:         bin
d/d 524460:     dev
l/l 14:         lib
d/d 524463:     proc
d/d 524464:     root
d/d 524465:     run
l/l 16:         sbin
d/d 393258:     sys
l/l 15:         lib64
d/d 524467:     tmp
d/d 524556:     mnt
d/d 524557:     srv
d/d 524558:     opt
d/d 524560:     media
r/r 64113:      .autorelabel
d/d 410038:     snap
V/V 1433601:    $OrphanFiles
```

O `fls` lista arquivos e diretórios presentes no sistema de arquivos, associando-os aos respectivos identificadores de inode.

Também foi observada a entrada:

```text
V/V 1433601:    $OrphanFiles
```

indicando a presença de estruturas associadas a arquivos órfãos identificadas pelo TSK.

### 5. Consulta de informações do inode

Foi executado:

```bash
ils /dev/nvme0n1p1 2
```

Saída:

```text
class|host|device|start_time
ils|kali||1765063051
st_ino|st_alloc|st_uid|st_gid|st_mtime|st_atime|st_ctime|st_crtime|st_mode|st_nlink|st_size
```

O valor `1765063051` corresponde ao momento em que a coleta foi iniciada. A conversão foi realizada com:

```bash
date -d @1765063051
```

Resultado:

```text
sáb 06 dez 2025 20:17:31 -03
```

A saída do `ils` apresenta campos relacionados ao inode, incluindo:

* `st_ino`: número do inode.
* `st_alloc`: informação de alocação do inode.
* `st_uid`: identificador do usuário proprietário.
* `st_gid`: identificador do grupo.
* `st_mtime`: timestamp de modificação.
* `st_atime`: timestamp de acesso.
* `st_ctime`: timestamp de alteração dos metadados.
* `st_crtime`: timestamp de criação, quando suportado pelo sistema de arquivos.
* `st_mode`: tipo e permissões.
* `st_nlink`: quantidade de links.
* `st_size`: tamanho associado ao inode.

## Conceitos

* **The Sleuth Kit (TSK):** conjunto de ferramentas para análise forense de sistemas de arquivos e mídias.
* **`fls`:** lista arquivos e diretórios identificados em uma imagem ou sistema de arquivos.
* **`ils`:** apresenta informações relacionadas aos inodes.
* **Inode:** estrutura que mantém metadados de arquivos e diretórios.
* **Timestamps:** informações temporais importantes para análise de eventos.

## Fluxo

```text
Partição
   ↓
fdisk -l
   ↓
Identificação de /dev/nvme0n1p1
   ↓
fls
   ↓
Listagem de arquivos/diretórios
   ↓
ils
   ↓
Informações de inode e timestamps
```

## Resultado

Foi possível utilizar ferramentas do TSK para listar estruturas do sistema de arquivos e consultar informações relacionadas a inodes, demonstrando uma base para análise forense de sistemas Linux.

## Evidência

[**Evidências — Módulo 12 / Aulas 43 e 44**](../evidencias.pdf)

**Print solicitado:** passo 5 — saída do `ils /dev/nvme0n1p1 2`.
