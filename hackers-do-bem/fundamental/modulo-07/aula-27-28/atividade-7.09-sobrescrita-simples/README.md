# Atividade 7.9 — Sobrescrita Simples no Kali Linux

## Objetivo

Realizar uma **sobrescrita simples** em uma partição no Kali Linux utilizando dados aleatórios, preenchendo o dispositivo até que não haja mais espaço disponível.

A atividade demonstra uma técnica de sobrescrita física de dados utilizando o comando `dd` e permite observar o estado do sistema de arquivos após a operação.

---

## Ambiente

* **Sistema:** Kali Linux
* **Disco utilizado:** `/dev/nvme1n1`
* **Partição utilizada:** `/dev/nvme1n1p1`
* **Sistema de arquivos:** `ext4`
* **Ferramentas:** `mkfs.ext4`, `mount`, `dd` e `df`

> A operação de sobrescrita foi realizada somente na partição disponibilizada para o laboratório.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo:

```bash id="q4m1sv"
sudo -i
```

---

## 2. Formatação e montagem da partição

A partição utilizada na atividade anterior foi formatada novamente com `ext4`:

```bash id="7m5q1n"
mkfs.ext4 /dev/nvme1n1p1
```

Saída:

```text id="8h1x5c"
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

Em seguida, foi criado o diretório que será utilizado como ponto de montagem:

```bash id="xq3j8f"
mkdir -m 777 /home/aluno/Documentos/MeuHD
mount /dev/nvme1n1p1 /home/aluno/Documentos/MeuHD
```

A partição passou a estar disponível através do diretório:

```text
/home/aluno/Documentos/MeuHD
```

---

## 3. Criação do arquivo de teste

Foi acessado o ponto de montagem:

```bash id="1w5r9c"
cd /home/aluno/Documentos/MeuHD
```

Em seguida, foi criado o arquivo:

```bash id="v2z8k4"
nano Teste.txt
```

Conteúdo inserido:

```text
Teste
```

Antes da sobrescrita, o conteúdo do diretório foi verificado:

```bash id="r6t0pf"
ls
```

Saída:

```text
lost+found  Teste.txt
```

O arquivo `Teste.txt` representa um dado existente na partição antes da execução da sobrescrita.

---

## 4. Sobrescrita com dados aleatórios

Para preencher a partição com dados provenientes de `/dev/urandom`, foi utilizado:

```bash id="c9m4wx"
dd if=/dev/urandom of=/dev/nvme1n1p1 bs=10M
```

Saída:

```text id="7bq3dz"
dd: erro de escrita de '/dev/nvme1n1p1': Não há espaço disponível no dispositivo
11+0 records in
10+0 records out
104857600 bytes (105 MB, 100 MiB) copied, 0,938747 s, 112 MB/s
```

### Interpretação

O comando utilizado foi:

```text
dd if=/dev/urandom of=/dev/nvme1n1p1 bs=10M
```

Cada parâmetro possui uma função específica:

* `dd` — realiza cópia de dados em baixo nível;
* `if=/dev/urandom` — define `/dev/urandom` como origem dos dados aleatórios;
* `of=/dev/nvme1n1p1` — define a partição como destino;
* `bs=10M` — utiliza blocos de 10 MiB por operação.

A execução continuou até que o dispositivo não tivesse mais espaço disponível para receber novos dados:

```text
dd: erro de escrita de '/dev/nvme1n1p1': Não há espaço disponível no dispositivo
```

A própria saída indica:

```text
10+0 records out
104857600 bytes (105 MB, 100 MiB) copied
```

Ou seja, foram efetivamente gravados **10 blocos de 10 MiB**, totalizando **100 MiB**.

O erro final ocorreu porque o comando tentou continuar escrevendo depois que o espaço disponível na partição foi preenchido.

---

## 5. Verificação do espaço utilizado

Após a sobrescrita, foi executado o comando:

```bash id="n7c2vp"
df -h
```

Saída registrada no laboratório:

```text id="w6p3sa"
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

A saída registrada mostra a partição `/dev/nvme1n1p1` com:

```text
948G  948G     0 100%
```

indicando que, de acordo com a saída obtida durante o laboratório, o dispositivo estava completamente ocupado.

> **Observação:** os valores de capacidade apresentados acima foram preservados conforme a saída registrada durante o laboratório, mesmo havendo uma inconsistência aparente com o tamanho de aproximadamente 100 MiB informado anteriormente para a partição.

---

## 6. Comportamento do sistema após a sobrescrita

Após o preenchimento da partição, a tentativa de listar novamente seu conteúdo apresentou a seguinte mensagem no ambiente do laboratório:

```text
ls: lendo o diretório '.': A estrutura necessita de limpeza
```

Isso demonstra que a sobrescrita direta no dispositivo alterou as estruturas que anteriormente pertenciam ao sistema de arquivos.

A operação foi realizada diretamente sobre:

```text
/dev/nvme1n1p1
```

e não através de um arquivo comum dentro do sistema de arquivos montado.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 7**, apresentando a saída do comando `df -h` após a sobrescrita.

[**Evidências — Módulo 7 / Aulas 27 e 28**](../evidencias.pdf)
