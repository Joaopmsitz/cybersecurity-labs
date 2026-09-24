# Atividade 1.1 — Comparando integridade de arquivos de texto

## Objetivo

Verificar a integridade de arquivos de texto por meio da comparação entre um arquivo original e uma cópia, identificando alterações realizadas após a cópia.

A atividade utiliza o comando `diff` do Linux para verificar se existem diferenças entre dois arquivos de texto.

## Ambiente

* Kali Linux
* Terminal
* Usuário `aluno`
* Diretório de trabalho: `/home/aluno/Documentos`
* Ferramentas utilizadas: `diff`, `cp`, `ls` e `nano`

## Procedimento

### 1. Criando o arquivo de texto

Foi criado um arquivo chamado `Texto.txt` utilizando o editor de texto do Kali Linux.

O conteúdo utilizado foi:

```text
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum. Aliquam nonummy auctor massa. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nulla at risus. Quisque purus magna, auctor et, sagittis ac, posuere eu, lectus. Nam mattis, felis ut adipiscing.
```

O arquivo foi salvo no diretório:

```text
/home/aluno/Documentos/
```

### 2. Acessando o terminal como superusuário

Foi aberto o Terminal Emulator e executado o seguinte comando:

```bash
sudo -i
```

Após a autenticação, o terminal passou a utilizar o usuário `root`.

### 3. Acessando o diretório dos arquivos

Foi acessado o diretório onde o arquivo `Texto.txt` foi salvo:

```bash
cd /home/aluno/Documentos/
```

Em seguida, foi utilizado o comando `ls` para verificar os arquivos presentes:

```bash
ls
```

O arquivo `Texto.txt` foi identificado no diretório.

### 4. Criando uma cópia do arquivo

Foi criada uma cópia do arquivo original utilizando o comando `cp`:

```bash
cp Texto.txt Texto_copia.txt
```

Depois, o comando `ls` foi utilizado novamente para confirmar a criação da cópia:

```bash
ls
```

Os dois arquivos passaram a estar presentes no diretório:

```text
Texto.txt
Texto_copia.txt
```

### 5. Comparando os arquivos antes da alteração

Com os dois arquivos ainda idênticos, foi executado:

```bash
diff Texto.txt Texto_copia.txt
```

O comando não apresentou nenhuma saída.

Isso indica que não foram encontradas diferenças entre os arquivos naquele momento.

### 6. Modificando a cópia

Para simular uma alteração no arquivo, a cópia foi aberta utilizando o editor `nano`:

```bash
nano Texto_copia.txt
```

A primeira letra `L` do texto foi alterada para `P`.

O início do conteúdo original:

```text
Lorem ipsum dolor sit amet...
```

passou a ser:

```text
Porem ipsum dolor sit amet...
```

Após a alteração, o arquivo foi salvo e o editor foi fechado.

### 7. Comparando novamente os arquivos

Após a modificação, o comando `diff` foi executado novamente:

```bash
diff Texto.txt Texto_copia.txt
```

Dessa vez, o comando identificou a diferença existente entre os arquivos.

A saída apresentada foi semelhante a:

```text
1c1
< Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum. Aliquam nonummy auctor massa. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nulla at risus. Quisque purus magna, auctor et, sagittis ac, posuere eu, lectus. Nam mattis, felis ut adipiscing.
---
> Porem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum. Aliquam nonummy auctor massa. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nulla at risus. Quisque purus magna, auctor et, sagittis ac, posuere eu, lectus. Nam mattis, felis ut adipiscing.
```

A saída pode apresentar pequenas diferenças dependendo do conteúdo utilizado e da versão do sistema.

## Interpretação do resultado

O comando `diff` compara o conteúdo dos arquivos e informa as diferenças encontradas.

* `1c1` indica uma alteração (`c`, de *change*) envolvendo a primeira linha dos arquivos.
* `<` identifica o conteúdo presente no arquivo original `Texto.txt`.
* `---` separa o conteúdo original do conteúdo modificado.
* `>` identifica o conteúdo presente no arquivo `Texto_copia.txt`.

Nesse caso, a diferença ocorreu na primeira linha, onde:

```text
Lorem
```

foi alterado para:

```text
Porem
```

A comparação demonstrou, portanto, que uma alteração realizada depois da criação da cópia pode ser identificada utilizando o comando `diff`.

## Comandos utilizados

```bash
sudo -i
cd /home/aluno/Documentos/
ls
cp Texto.txt Texto_copia.txt
ls
diff Texto.txt Texto_copia.txt
nano Texto_copia.txt
diff Texto.txt Texto_copia.txt
```

## Resultado

Foi possível verificar a integridade de um arquivo de texto comparando-o com uma cópia.

Na primeira comparação, os arquivos eram idênticos e o `diff` não apresentou saída. Após a alteração do arquivo `Texto_copia.txt`, uma nova comparação identificou exatamente a linha modificada.

## Conceitos praticados

* Integridade de arquivos
* Comparação de arquivos
* Identificação de alterações
* Linux
* Terminal
* `diff`
* `cp`
* `ls`
* `nano`
* Manipulação de arquivos pela linha de comando

## Evidência

A evidência visual solicitada pelo curso está disponível no PDF de evidências da Aula 01–02.

O print corresponde à execução do comando `diff` após a alteração do arquivo `Texto_copia.txt`, demonstrando a diferença encontrada entre o arquivo original e sua cópia.

[Ver evidências — Aula 01–02](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-01-02/evidencias.pdf)

