# Atividade 8.6 — Computando Hash MD5, RIPEMD-160 e Blake2

## Objetivo

Calcular o **hash** de um arquivo utilizando diferentes algoritmos de resumo criptográfico no Kali Linux:

* MD5;
* RIPEMD-160;
* Blake2.

A atividade permite comparar os diferentes tamanhos dos resumos gerados e observar como cada algoritmo produz uma representação hexadecimal do conteúdo do arquivo.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramentas:** `md5sum`, `openssl` e `b2sum`
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo analisado:** `mensagem.txt`
* **Conteúdo:** `Hackers do bem!`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash
sudo -i
```

---

## 2. Acesso ao diretório de trabalho

Foi acessada a pasta `Arquivos`:

```bash
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi criado o arquivo de texto:

```bash
nano mensagem.txt
```

O conteúdo inserido foi:

```text
Hackers do bem!
```

---

## 3. Verificação do arquivo

Após a criação, foi utilizado `ls` para verificar a presença do arquivo:

```bash
ls
```

Saída:

```text
mensagem.txt
```

O arquivo `mensagem.txt` passou a ser a entrada utilizada nos cálculos dos diferentes hashes.

---

## 4. Cálculo do hash MD5

Foi utilizado o comando `md5sum`:

```bash
md5sum mensagem.txt
```

Saída:

```text
ac640793b0fe42e14c071f53fe8f8486  mensagem.txt
```

O resultado possui **32 caracteres hexadecimais**, correspondentes a 128 bits.

O comando `md5sum` calcula o resumo MD5 do conteúdo do arquivo e apresenta o resultado junto ao nome do arquivo processado.

---

## 5. Cálculo do hash RIPEMD-160

Em seguida, foi utilizado o OpenSSL para calcular o RIPEMD-160:

```bash
openssl dgst -ripemd160 mensagem.txt
```

Saída:

```text
RIPEMD-160(mensagem.txt)= 1ec06a94e04fc961bad8957e1fd1f27af9dd421d
```

O resultado possui **40 caracteres hexadecimais**, correspondentes a 160 bits.

O comando `openssl dgst` calcula o resumo criptográfico utilizando o algoritmo especificado, neste caso, `-ripemd160`.

---

## 6. Cálculo do hash Blake2

Por fim, foi utilizado o `b2sum` para calcular o hash Blake2:

```bash
b2sum mensagem.txt
```

Saída:

```text
a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98  mensagem.txt
```

O resultado possui **128 caracteres hexadecimais**, correspondentes a 512 bits.

---

## 7. Evidência — Blake2

A evidência solicitada para esta atividade corresponde ao **passo 7**, no qual é calculado o hash Blake2 do arquivo `mensagem.txt`:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# b2sum mensagem.txt 
a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98  mensagem.txt
```

[**Evidências — Módulo 8 / Aulas 31 e 32**](../evidencias.pdf)

---

## Comparação dos resultados

| Algoritmo  | Tamanho do resumo | Hash obtido                                                                                                                        |
| ---------- | ----------------: | ---------------------------------------------------------------------------------------------------------------------------------- |
| MD5        |          128 bits | `ac640793b0fe42e14c071f53fe8f8486`                                                                                                 |
| RIPEMD-160 |          160 bits | `1ec06a94e04fc961bad8957e1fd1f27af9dd421d`                                                                                         |
| Blake2     |          512 bits | `a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98` |

Os três algoritmos produziram resumos diferentes para o mesmo arquivo, com tamanhos distintos.

O **MD5** e o **RIPEMD-160** são algoritmos históricos que não devem ser escolhidos para novas aplicações que dependam de resistência moderna a colisões. A família **BLAKE2** foi projetada posteriormente e possui variantes com diferentes tamanhos de saída, sendo o `b2sum` utilizado nesta atividade para produzir um resumo de 512 bits.

---

## Resultado

A atividade demonstrou, na prática, como calcular diferentes funções de hash sobre um mesmo arquivo utilizando ferramentas disponíveis no Kali Linux. Os valores obtidos podem ser utilizados para verificar se o conteúdo de um arquivo permanece inalterado: qualquer alteração no conteúdo tende a produzir um resumo diferente.
