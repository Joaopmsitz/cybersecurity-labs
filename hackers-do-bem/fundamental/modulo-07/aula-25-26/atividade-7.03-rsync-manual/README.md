# Atividade 7.3 — Rsync Manual

## Objetivo

Realizar uma cópia manual de arquivo entre dois diretórios utilizando o `rsync`, entendendo os principais parâmetros do comando e verificando a integridade da cópia.

---

## 1. Preparação dos diretórios

Foi utilizado o diretório `/home/aluno/Documentos/` como base para o laboratório.

```bash
sudo -i
cd /home/aluno/Documentos/
mkdir -m 777 PastaA PastaB
ls
```

Saída:

```text
PastaA  PastaB
```

A estrutura utilizada ficou:

```text
/home/aluno/Documentos/
├── PastaA/
└── PastaB/
```

---

## 2. Criação do arquivo de teste

Dentro da `PastaA`, foi criado o arquivo `Teste.txt`:

```bash
cd PastaA
nano Teste.txt
```

Conteúdo:

```text
Teste de Pasta A para Pasta B
```

Após salvar o arquivo:

```bash
ls
```

Saída:

```text
Teste.txt
```

Em seguida, foi acessado o diretório de destino:

```bash
cd /home/aluno/Documentos/PastaB
ls
```

Neste momento, a `PastaB` estava vazia.

---

## 3. Cópia utilizando Rsync

Foi utilizado o seguinte comando para copiar o arquivo da `PastaA` para a `PastaB`:

```bash
rsync -avz /home/aluno/Documentos/PastaA/Teste.txt /home/aluno/Documentos/PastaB
```

Saída:

```text
sending incremental file list
Teste.txt

sent 140 bytes  received 35 bytes  350,00 bytes/sec
total size is 30  speedup is 0,17
```

### Parâmetros utilizados

* `rsync` — ferramenta utilizada para sincronização e transferência de arquivos.
* `-a` — modo *archive*, mantendo atributos como permissões, proprietários, grupos e timestamps, além de permitir cópia recursiva.
* `-v` — modo *verbose*, exibindo informações sobre a operação.
* `-z` — utiliza compressão durante a transferência.
* `/home/aluno/Documentos/PastaA/Teste.txt` — arquivo de origem.
* `/home/aluno/Documentos/PastaB` — diretório de destino.

---

## 4. Verificação da cópia

Após a execução do `rsync`, foi verificado o conteúdo da `PastaB`:

```bash
ls
```

Saída:

```text
Teste.txt
```

Em seguida, o conteúdo do arquivo foi conferido:

```bash
cat Teste.txt
```

Resultado:

```text
Teste de Pasta A para Pasta B
```

A cópia foi realizada corretamente e o conteúdo permaneceu igual ao arquivo original.

---

## 5. Limpeza do diretório de destino

Para preparar o ambiente para a próxima atividade, o arquivo copiado foi removido somente da `PastaB`:

```bash
ls
Teste.txt
rm *
```

O sistema solicitou confirmação:

```text
zsh: sure you want to delete the only file in /home/aluno/Documentos/PastaB [yn]? y
```

Depois:

```bash
ls
```

A `PastaB` ficou novamente vazia.

O arquivo `Teste.txt` da `PastaA` foi mantido, pois será utilizado na atividade seguinte.

---

## Evidência

[**Evidências — Módulo 7 / Aulas 1 e 2**](../evidencias.pdf)
