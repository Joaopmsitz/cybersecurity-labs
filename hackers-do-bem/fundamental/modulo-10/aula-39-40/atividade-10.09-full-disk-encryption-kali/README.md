# Atividade 10.9 — Full Disk Encryption em uma Partição no Kali Linux

## Objetivo

Implementar criptografia em uma partição no Kali Linux utilizando **LUKS (Linux Unified Key Setup)**, criando uma partição dedicada, protegendo-a com senha, formatando-a com ext4 e realizando sua montagem e desmontagem.

> Apesar de o laboratório utilizar o termo **Full Disk Encryption (FDE)**, nesta atividade a criptografia foi aplicada especificamente à partição `/dev/nvme1n1p3`, e não ao disco inteiro.

---

## Ambiente

* **Sistema:** Kali GNU/Linux Rolling
* **Acesso:** RDP
* **Disco principal:** `/dev/nvme0n1`
* **Disco utilizado na atividade:** `/dev/nvme1n1`
* **Partição criada:** `/dev/nvme1n1p3`
* **Tamanho da nova partição:** 200 MiB
* **Tecnologia de criptografia:** LUKS
* **Sistema de arquivos:** ext4
* **Mapeamento criptográfico:** `Teste`
* **Ponto de montagem:** `/mnt/encrypted`

---

## 1. Acessando o Kali Linux

A máquina Kali Linux foi iniciada e acessada remotamente.

Após o acesso, foi aberto um terminal e obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Identificando os discos e partições

Foi utilizado o comando:

```bash
fdisk -l
```

A saída apresentou dois discos. O disco principal era `/dev/nvme0n1`, enquanto o disco utilizado na atividade era `/dev/nvme1n1`.

A saída referente ao disco utilizado foi:

```text id="qa904k"
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

Foi identificado que `/dev/nvme1n1` possuía espaço disponível para a criação de uma nova partição.

---

## 3. Acessando o disco pelo fdisk

Foi utilizado:

```bash
fdisk /dev/nvme1n1
```

Dentro do `fdisk`, foi utilizado `p` para visualizar a tabela de partições:

```text id="mebhb5"
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

## 4. Criando uma nova partição

Foi utilizada a opção `n` para criar uma nova partição primária.

A configuração utilizada foi:

* Número da partição: `3`
* Primeiro setor: padrão
* Último setor: `+200M`
* Tipo: Linux

A saída apresentada foi:

```text id="498rxr"
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

A nova partição criada foi:

```text
/dev/nvme1n1p3
```

com tamanho de aproximadamente **200 MiB**.

---

## 5. Verificando e gravando a tabela de partições

Foi utilizado novamente `p` para verificar a configuração:

```text id="jqjw87"
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

Depois de sair do `fdisk`, foi executado:

```bash
partprobe /dev/nvme1n1
```

O `partprobe` solicita ao sistema que releia a tabela de partições, permitindo que a nova partição seja reconhecida sem reinicializar a máquina.

---

## 6. Inicializando a criptografia LUKS

A partição criada foi configurada para utilizar LUKS através do comando:

```bash
cryptsetup luksFormat /dev/nvme1n1p3
```

O `cryptsetup` apresentou um aviso informando que a operação sobrescreveria permanentemente os dados existentes na partição.

```text id="2nvjxk"
WARNING!
========
Isto vai sobrescrever dados em /dev/nvme1n1p3 permanentemente.

Are you sure? (Type 'yes' in capital letters): YES
Digite a senha para /dev/nvme1n1p3: 
Verificar senha:
```

Foi definida uma senha para proteger o volume criptografado.

> A senha utilizada no laboratório não é registrada neste README.

---

## 7. Abrindo o volume criptografado

Após a inicialização do LUKS, a partição foi aberta com:

```bash
cryptsetup luksOpen /dev/nvme1n1p3 Teste
```

O nome `Teste` foi utilizado como identificador do mapeamento do dispositivo criptografado.

Com isso, o volume passou a ser acessível através de:

```text
/dev/mapper/Teste
```

---

## 8. Criando o sistema de arquivos ext4

O volume criptografado foi formatado utilizando ext4:

```bash
mkfs.ext4 /dev/mapper/Teste
```

A saída apresentada foi:

```text id="a6ghof"
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

Nesse momento, o sistema de arquivos ext4 foi criado sobre o dispositivo mapeado pelo LUKS.

---

## 9. Criando o ponto de montagem

Foi criado o diretório que seria utilizado para acessar o volume:

```bash
mkdir -m 777 /mnt/encrypted
```

A opção `-m 777` definiu as permissões do diretório de acordo com o procedimento proposto no laboratório.

---

## 10. Montando o volume criptografado

O volume foi montado utilizando:

```bash
mount /dev/mapper/Teste /mnt/encrypted
```

Com isso, o conteúdo do sistema de arquivos criptografado passou a estar disponível através de:

```text
/mnt/encrypted
```

---

## 11. Desmontando o volume

Após a utilização do volume, ele foi desmontado com:

```bash
umount /mnt/encrypted
```

Esse procedimento encerra o acesso ao sistema de arquivos através do ponto de montagem.

---

## 12. Verificando o volume pelo ambiente gráfico

Após a desmontagem, foi observada no desktop a unidade:

```text
Volume de 193MB
```

O volume foi acessado pelo ambiente gráfico, abrindo o ícone correspondente para visualizar a pasta no **Thunar**.

### Evidência — Passo 12

**Frase obrigatória antes do print:**

> **Print da atividade 10.9:** volume criptografado `Volume de 193MB` exibido no desktop do Kali Linux e acessado pelo gerenciador de arquivos Thunar.

[**Evidências — Módulo 10 / Aulas 39 e 40**](../evidencias.pdf)

Após o registro da evidência, o Thunar e o terminal foram fechados.

---

## Conceitos

* **LUKS:** padrão utilizado no Linux para implementar criptografia de dispositivos de bloco.
* **cryptsetup:** ferramenta utilizada para configurar e abrir volumes LUKS.
* **`/dev/mapper/Teste`:** dispositivo lógico disponibilizado após abrir o volume criptografado.
* **ext4:** sistema de arquivos criado sobre o volume criptografado.
* **mount/umount:** comandos utilizados para montar e desmontar o sistema de arquivos.

## Fluxo da atividade

```text
Identificar disco
      ↓
Criar /dev/nvme1n1p3
      ↓
Configurar LUKS
      ↓
Abrir volume criptografado
      ↓
Criar filesystem ext4
      ↓
Montar em /mnt/encrypted
      ↓
Desmontar
      ↓
Verificar volume no Thunar
```

## Resultado

Foi criada a partição `/dev/nvme1n1p3`, configurada com **LUKS**, aberta através do `cryptsetup` e formatada com **ext4**. O volume foi montado, desmontado e posteriormente identificado no ambiente gráfico do Kali Linux.
