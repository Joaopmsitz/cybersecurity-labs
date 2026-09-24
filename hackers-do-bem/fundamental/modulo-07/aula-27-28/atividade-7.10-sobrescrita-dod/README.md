# Atividade 7.10 — Sobrescrita com Padrão DoD 5220.22-M

## Objetivo

Realizar uma sobrescrita de dados em uma partição utilizando o comando `shred`, aplicando uma passagem de dados aleatórios seguida de uma passagem com zeros.

A atividade utiliza como referência o padrão **DoD 5220.22-M**, apresentado no laboratório como contexto para a técnica de sobrescrita.

---

## Ambiente

* **Sistema:** Kali Linux
* **Disco utilizado:** `/dev/nvme1n1`
* **Partições existentes:** `/dev/nvme1n1p1` e `/dev/nvme1n1p2`
* **Ferramenta:** `shred`
* **Partição utilizada para a sobrescrita:** `/dev/nvme1n1p2`

> A operação foi realizada somente na partição disponibilizada para o laboratório.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo:

```bash id="4h6m1p"
sudo -i
```

---

## 2. Verificação do disco

Foi utilizado o `fdisk` para verificar a tabela de partições do disco:

```bash id="8w2j4k"
fdisk /dev/nvme1n1
```

Dentro do `fdisk`, foi utilizado o comando `p` para exibir as partições:

```text id="v7q1cs"
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

A saída mostra que a partição existente `nvme1n1p1` ocupa 100 MiB.

---

## 3. Criação da segunda partição

Dentro do `fdisk`, foi criada uma nova partição primária:

```text id="m8e2rf"
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

A nova partição criada foi:

```text id="i3g5wl"
/dev/nvme1n1p2
```

com tamanho de **100 MiB**.

---

## 4. Gravação da tabela de partições

As alterações foram gravadas utilizando o comando `w`:

```text id="v9m4xq"
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

Depois, a tabela de partições foi atualizada no kernel:

```bash id="4t8z1c"
partprobe /dev/nvme1n1
```

---

## 5. Verificação das partições

A estrutura dos dispositivos foi verificada com:

```bash id="c2x6vn"
lsblk
```

Saída:

```text id="9h4q3w"
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
nvme1n1      259:0    0    2G  0 disk 
├─nvme1n1p2  259:5    0  100M  0 part 
└─nvme1n1p1  259:6    0  100M  0 part /home/aluno/Documentos/MeuHD
nvme0n1      259:1    0   20G  0 disk 
├─nvme0n1p1  259:2    0 19,9G  0 part /
├─nvme0n1p14 259:3    0    3M  0 part 
└─nvme0n1p15 259:4    0  124M  0 part /boot/efi
```

A saída confirma a existência da nova partição:

```text id="e1v8bc"
/dev/nvme1n1p2  100M
```

Ela será utilizada como destino da sobrescrita.

---

## 6. Sobrescrita com `shred`

Foi executado o comando solicitado no laboratório:

```bash id="a9r4ks"
shred -vfz -n 1 /dev/nvme1n1p2
```

Saída:

```text id="6z3w1q"
shred: /dev/nvme1n1p2: passagem 1/2 (random)...
shred: /dev/nvme1n1p2: passagem 2/2 (000000)...
```

### Interpretação do comando

O comando utilizado foi:

```text id="m0q7dx"
shred -vfz -n 1 /dev/nvme1n1p2
```

Cada opção possui uma função:

* `-v` — exibe informações detalhadas durante a execução;
* `-f` — força a alteração das permissões quando necessário;
* `-z` — realiza uma passagem final preenchendo o dispositivo com zeros;
* `-n 1` — realiza uma passagem de sobrescrita com dados pseudorrandômicos;
* `/dev/nvme1n1p2` — dispositivo que será sobrescrito.

A saída demonstra as duas passagens realizadas:

```text id="d5q9hc"
passagem 1/2 (random)
passagem 2/2 (000000)
```

Portanto, nessa execução, o `shred` realizou uma passagem com dados aleatórios e uma segunda passagem preenchendo a área com zeros.

---

## Observação técnica sobre o DoD 5220.22-M

O laboratório apresenta essa técnica no contexto do padrão **DoD 5220.22-M**. Entretanto, tecnicamente, o comando executado:

```bash id="k8v3fz"
shred -vfz -n 1 /dev/nvme1n1p2
```

não deve ser interpretado como uma implementação completa ou como uma certificação de conformidade com o padrão.

Com `-n 1` e `-z`, a operação realizada consiste em:

1. uma passagem com dados pseudorrandômicos;
2. uma passagem final com zeros.

O objetivo prático no laboratório é demonstrar o conceito de **sobrescrita de dados**, dificultando a recuperação do conteúdo anteriormente armazenado na área sobrescrita.

Além disso, técnicas de sobrescrita podem ter limitações em determinados tipos de armazenamento, especialmente SSDs e dispositivos com mecanismos internos de gerenciamento de blocos.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 6**, apresentando a execução do comando `shred` e as duas passagens realizadas.

[**Evidências — Módulo 7 / Aulas 27 e 28**](../evidencias.pdf)
