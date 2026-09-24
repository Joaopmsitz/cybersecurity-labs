# Atividade 1.3 — Verificando integridade de arquivos com função Hash

## Objetivo

Verificar a integridade de arquivos utilizando uma função de Hash, comparando os valores gerados pelo algoritmo MD5 para arquivos idênticos e arquivos que sofreram alterações.

A atividade utiliza o comando `md5sum` do Kali Linux para calcular o hash MD5 dos arquivos e demonstrar como uma alteração no conteúdo resulta em um valor de hash diferente.

## Ambiente

* Kali Linux
* Terminal
* Usuário `aluno`
* Diretório de trabalho: `/home/aluno/Documentos`
* Ferramenta utilizada: `md5sum`

## Procedimento

### 1. Acessando o terminal como superusuário

Foi aberto o Terminal Emulator e executado:

```bash
sudo -i
```

Após a autenticação, o terminal passou a utilizar o usuário `root`.

### 2. Acessando o diretório dos arquivos

Os arquivos utilizados nas atividades anteriores foram armazenados no diretório `Documentos`.

Para acessar o diretório:

```bash
cd /home/aluno/Documentos/
```

### 3. Verificando os arquivos disponíveis

Foi utilizado o comando:

```bash
ls
```

Os arquivos criados nas atividades anteriores foram identificados no diretório:

```text
Imagem1.png
Imagem1_copia.png
Imagem2.png
Texto.txt
Texto_copia.txt
```

### 4. Calculando o Hash MD5

O comando `md5sum` foi utilizado para calcular o hash de cada arquivo.

Para `Imagem1.png`:

```bash
md5sum Imagem1.png
```

Para `Imagem1_copia.png`:

```bash
md5sum Imagem1_copia.png
```

Para `Imagem2.png`:

```bash
md5sum Imagem2.png
```

Para `Texto.txt`:

```bash
md5sum Texto.txt
```

Para `Texto_copia.txt`:

```bash
md5sum Texto_copia.txt
```

Os valores hexadecimais retornados são específicos para os arquivos utilizados durante a execução da atividade e podem ser diferentes em outras execuções.

### 5. Comparando os hashes

Os valores retornados pelo `md5sum` foram comparados para verificar a integridade dos arquivos.

`Imagem1.png` e `Imagem1_copia.png` apresentaram o mesmo valor de hash, pois eram arquivos idênticos.

Já `Imagem2.png` apresentou um valor diferente, pois a imagem havia recebido uma alteração.

Da mesma forma, `Texto.txt` e `Texto_copia.txt` apresentaram hashes diferentes porque o conteúdo da cópia havia sido modificado na Atividade 1.1.

## Interpretação do resultado

O MD5 gera um valor hexadecimal a partir do conteúdo de um arquivo.

Quando dois arquivos possuem o mesmo conteúdo, o resultado do MD5 tende a ser o mesmo. Quando o conteúdo é alterado, o valor calculado também muda.

Neste laboratório:

```text
Imagem1.png
Imagem1_copia.png
```

possuíam o mesmo hash porque os arquivos eram idênticos.

Já:

```text
Imagem1.png
Imagem2.png
```

possuíam hashes diferentes devido à alteração realizada na imagem.

O mesmo comportamento foi observado nos arquivos de texto:

```text
Texto.txt
Texto_copia.txt
```

A alteração realizada anteriormente na cópia fez com que os valores de hash fossem diferentes.

> **Observação:** MD5 é útil para demonstrar o conceito de verificação de integridade neste laboratório, mas não é considerado adequado para aplicações modernas que dependem de resistência a colisões criptográficas. Para usos atuais de segurança, algoritmos mais robustos, como SHA-256, são preferíveis.

## Comandos utilizados

```bash
sudo -i
cd /home/aluno/Documentos/
ls
md5sum Imagem1.png
md5sum Imagem1_copia.png
md5sum Imagem2.png
md5sum Texto.txt
md5sum Texto_copia.txt
```

## Limpeza do ambiente

Após a realização dos testes, os arquivos utilizados foram removidos com:

```bash
rm *
```

O sistema solicitou confirmação antes da remoção dos arquivos.

Depois, foi utilizado:

```bash
ls
```

para verificar o conteúdo restante do diretório.

## Resultado

Foi possível utilizar o algoritmo MD5 para comparar a integridade dos arquivos.

Os arquivos idênticos apresentaram o mesmo hash, enquanto os arquivos que sofreram alterações apresentaram valores diferentes.

A atividade demonstrou, na prática, como funções de hash podem ser utilizadas para identificar alterações no conteúdo de arquivos.

## Conceitos praticados

* Integridade de arquivos
* Funções de Hash
* MD5
* Verificação de integridade
* Comparação de valores hash
* Linux
* Terminal
* `md5sum`
* `rm`
* `ls`

## Evidência

A evidência visual solicitada pelo curso está disponível no PDF de evidências da Aula 01–02.

O print corresponde à execução dos comandos `md5sum` e apresenta os valores de hash calculados para os arquivos utilizados na atividade.

[Ver evidências — Aula 01–02](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-01-02/evidencias.pdf)
