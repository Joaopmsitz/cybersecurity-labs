# Atividade 12.10 — Aquisição de imagem de disco no Kali Linux

Nesta atividade foi realizada a aquisição de uma partição utilizando o comando **dd**, criando uma cópia em nível de bloco da partição `/dev/nvme1n1p3` em um arquivo.

> **Observação:** credenciais utilizadas no ambiente de laboratório não são registradas neste documento.

## Objetivo

* Identificar partições disponíveis no sistema.
* Utilizar o `dd` para realizar uma cópia em nível de bloco.
* Criar uma imagem da partição em um arquivo.
* Verificar o tamanho e os atributos do arquivo adquirido.

## Procedimento

### 1. Acesso ao Kali Linux

O Kali Linux foi acessado via RDP pelo endereço `192.168.98.40`.

Foi obtido acesso administrativo:

```bash
sudo -i
```

### 2. Identificação das partições

Foi executado:

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

A partição escolhida para a aquisição foi:

```text
/dev/nvme1n1p3
```

### 3. Aquisição da partição

Foi utilizado o `dd` para copiar o conteúdo da partição para um arquivo:

```bash
dd if=/dev/nvme1n1p3 of=/home/aluno/Documentos/Arquivos/Backup_nvme1n1p3
```

Saída:

```text
409600+0 registos entrados
409600+0 registos saídos
209715200 bytes (210 MB, 200 MiB) copiados, 1,58606 s, 132 MB/s
```

Os principais parâmetros utilizados foram:

* `dd`: ferramenta para operações de cópia em nível de bloco.
* `if=/dev/nvme1n1p3`: dispositivo de entrada, correspondente à partição analisada.
* `of=/home/aluno/Documentos/Arquivos/Backup_nvme1n1p3`: arquivo de saída que recebeu a cópia.

O resultado indica que foram processados `209715200` bytes, equivalentes a aproximadamente **200 MiB**, com taxa média de transferência de `132 MB/s`.

### 4. Verificação do arquivo

Foi acessado o diretório de destino:

```bash
cd /home/aluno/Documentos/Arquivos
```

Em seguida:

```bash
ls
```

Resultado:

```text
Backup_nvme1n1p3
```

### 5. Análise dos atributos do arquivo

Foi utilizado o comando `stat`:

```bash
stat Backup_nvme1n1p3
```

Saída:

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

A saída permite observar o tamanho da imagem, quantidade de blocos, inode, permissões, proprietário e timestamps do arquivo criado.

### 6. Remoção da imagem

Após a verificação, o arquivo de aquisição foi removido:

```bash
rm Backup_nvme1n1p3
```

A pasta foi conferida novamente:

```bash
ls
```

O arquivo de backup não estava mais presente.

## Conceitos

* **Aquisição de imagem:** criação de uma cópia dos dados de uma mídia ou partição para análise.
* **`dd`:** realiza cópia em nível de bloco.
* **`if`:** define a origem dos dados.
* **`of`:** define o destino.
* **`stat`:** apresenta atributos e timestamps do arquivo.
* **Imagem forense:** pode ser utilizada como fonte para análise sem trabalhar diretamente sobre a mídia original.

## Fluxo

```text
Partição
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
Verificação da aquisição
   ↓
Remoção do arquivo
```

## Resultado

Foi realizada uma cópia em nível de bloco da partição `/dev/nvme1n1p3`, gerando um arquivo de `209715200` bytes. O arquivo foi posteriormente verificado com `stat` e removido ao final da atividade.

## Evidência

[**Evidências — Módulo 12 / Aulas 43 e 44**](../evidencias.pdf)

**Print solicitado:** passo 5 — saída do comando `stat Backup_nvme1n1p3`.
