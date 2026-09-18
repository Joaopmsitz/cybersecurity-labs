# Atividade 1.2 — Comparando integridade de arquivos genéricos

## Objetivo

Verificar a integridade de arquivos genéricos, utilizando imagens como exemplo, por meio da comparação entre arquivos idênticos e arquivos que sofreram alterações.

Nesta atividade foi utilizado o comando `cmp` do Linux para identificar diferenças entre arquivos binários.

## Ambiente

* Kali Linux
* Terminal
* KolourPaint
* Usuário `aluno`
* Diretório de trabalho: `/home/aluno/Documentos`
* Ferramentas utilizadas: `cmp`, `cd` e `ls`

## Procedimento

### 1. Abrindo o KolourPaint

O KolourPaint foi iniciado pelo terminal utilizando:

```bash
kolourpaint
```

### 2. Criando a primeira imagem

No KolourPaint, foi criada uma imagem utilizando diferentes cores e desenhos livres.

A imagem foi salva no diretório `Documentos` com o nome:

```text
Imagem1.png
```

### 3. Criando uma cópia da imagem

A mesma imagem foi salva novamente, sem nenhuma alteração, com o nome:

```text
Imagem1_copia.png
```

Dessa forma, `Imagem1.png` e `Imagem1_copia.png` deveriam possuir exatamente o mesmo conteúdo.

### 4. Modificando a imagem

Após criar a cópia, foi realizada uma pequena alteração na imagem original, adicionando um ponto utilizando uma das cores disponíveis no KolourPaint.

A imagem modificada foi salva como:

```text
Imagem2.png
```

Nesse momento, foram obtidos três arquivos:

```text
Imagem1.png
Imagem1_copia.png
Imagem2.png
```

`Imagem1.png` e `Imagem1_copia.png` são cópias idênticas, enquanto `Imagem2.png` contém uma alteração.

### 5. Verificando os arquivos no terminal

Após fechar o KolourPaint, foi acessado o diretório onde as imagens foram armazenadas:

```bash
cd /home/aluno/Documentos
```

Em seguida, foi utilizado:

```bash
ls
```

A listagem apresentou os arquivos criados na atividade, juntamente com os arquivos utilizados anteriormente na Atividade 1.1.

Exemplo:

```text
Imagem1_copia.png
Imagem1.png
Imagem2.png
Texto_copia.txt
Texto.txt
```

### 6. Comparando arquivos idênticos

Para verificar se `Imagem1.png` e `Imagem1_copia.png` possuíam diferenças, foi utilizado:

```bash
cmp Imagem1.png Imagem1_copia.png
```

O comando não apresentou nenhuma saída.

No `cmp`, a ausência de saída indica que nenhum byte diferente foi encontrado entre os dois arquivos.

Portanto, as duas imagens possuíam conteúdo idêntico.

### 7. Comparando arquivos modificados

Em seguida, foi realizada a comparação entre `Imagem1.png` e `Imagem2.png`:

```bash
cmp Imagem1.png Imagem2.png
```

Como `Imagem2.png` havia recebido uma alteração, o comando identificou uma diferença entre os arquivos.

Um resultado possível é semelhante a:

```text
Imagem1.png e Imagem2.png são diferentes: byte 58, linha 3
```

Os valores apresentados podem variar dependendo do conteúdo da imagem e da alteração realizada.

## Interpretação do resultado

O comando `cmp` realiza uma comparação byte a byte entre dois arquivos.

Na primeira comparação:

```bash
cmp Imagem1.png Imagem1_copia.png
```

não houve saída, indicando que os arquivos eram idênticos.

Na segunda comparação:

```bash
cmp Imagem1.png Imagem2.png
```

foi identificada uma diferença, pois `Imagem2.png` havia sido modificada.

Quando o comando informa, por exemplo:

```text
byte 58, linha 3
```

ele está indicando a posição aproximada em que a diferença foi encontrada.

Como estamos trabalhando com arquivos de imagem, que são arquivos binários, o termo `linha` não deve ser interpretado da mesma forma que uma linha de um arquivo de texto.

## Comandos utilizados

```bash
kolourpaint
cd /home/aluno/Documentos
ls
cmp Imagem1.png Imagem1_copia.png
cmp Imagem1.png Imagem2.png
```

## Resultado

Foi possível verificar a integridade de arquivos de imagem por meio da comparação byte a byte.

A comparação entre `Imagem1.png` e `Imagem1_copia.png` não encontrou diferenças, pois os arquivos eram idênticos.

Já a comparação entre `Imagem1.png` e `Imagem2.png` identificou uma diferença, demonstrando que uma pequena alteração no conteúdo da imagem pode ser detectada pelo comando `cmp`.

## Conceitos praticados

* Integridade de arquivos
* Comparação de arquivos binários
* Comparação byte a byte
* Linux
* Terminal
* `cmp`
* `ls`
* `cd`
* Identificação de alterações em arquivos
* Arquivos de imagem

## Evidência

A evidência visual solicitada pelo curso está disponível no PDF de evidências da Aula 01–02.

O print corresponde à execução do comando `cmp` entre `Imagem1.png` e `Imagem2.png`, demonstrando a diferença encontrada entre os arquivos.

[Ver evidências — Aula 01–02](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-01-02/evidencias.pdf)
