# Atividade 8.9 — ECC-256 para Confidencialidade

## Objetivo

Utilizar criptografia baseada em **Curvas Elípticas (ECC)** para demonstrar um processo de proteção e recuperação de uma mensagem.

Na atividade são utilizados:

* ECC com a curva `prime256v1`;
* chave privada;
* chave pública;
* derivação de uma chave compartilhada;
* AES-256-CBC para criptografia da mensagem;
* recuperação do conteúdo original utilizando a chave de sessão.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Curva ECC:** `prime256v1`
* **Criptografia simétrica:** AES-256-CBC
* **Diretório:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `mensagem.txt`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash id="1hj2qd"
sudo -i
```

---

## 2. Acesso ao diretório e verificação da mensagem

Foi acessado o diretório utilizado na atividade:

```bash id="z5s6yq"
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi verificada a presença da mensagem:

```bash id="e0k2qa"
ls
```

Saída:

```text id="l9c9hd"
mensagem.txt
```

O arquivo `mensagem.txt` foi utilizado como conteúdo de entrada para a criptografia.

---

## 3. Geração da chave privada ECC

Foi gerada uma chave privada utilizando a curva elíptica `prime256v1`:

```bash id="n4z0x1"
openssl ecparam -name prime256v1 -genkey -noout -out chave_privada.pem
```

A chave privada foi armazenada em:

```text id="c7m5km"
chave_privada.pem
```

Essa chave deve ser mantida em segurança e não deve ser compartilhada.

---

## 4. Geração da chave pública

A chave pública correspondente foi obtida a partir da chave privada:

```bash id="0d2h5w"
openssl ec -in chave_privada.pem -pubout -out chave_publica.pem
```

Saída:

```text id="o0a1p5"
read EC key
writing EC key
```

A estrutura de arquivos passou a ser:

```bash id="2t5i3q"
ls
```

Saída:

```text id="h8v4h2"
chave_privada.pem  chave_publica.pem  mensagem.txt
```

A chave pública pode ser compartilhada, enquanto a chave privada deve permanecer protegida.

---

## 5. Geração das chaves utilizadas na criptografia

Primeiramente, foi gerada uma chave de sessão aleatória de 32 bytes:

```bash id="v2m7qa"
openssl rand -out chave_sessao.bin 32
```

Em seguida, foi realizada uma operação de derivação utilizando as chaves ECC:

```bash id="p4x1jc"
openssl pkeyutl -derive -inkey chave_privada.pem -peerkey chave_publica.pem -out chave_compartilhada.bin
```

A verificação dos arquivos gerados apresentou:

```bash id="c8z5vq"
ls
```

Saída:

```text id="j9d6bw"
chave_compartilhada.bin chave_privada.pem chave_publica.pem chave_sessao.bin mensagem.txt
```

Nesse ponto, existem dois arquivos relacionados a chaves:

* `chave_sessao.bin` — chave aleatória de 32 bytes;
* `chave_compartilhada.bin` — resultado da operação de derivação ECC.

---

## 6. Criptografia da mensagem com AES-256-CBC

A mensagem foi criptografada utilizando AES-256-CBC:

```bash id="k0z4nq"
openssl enc -aes-256-cbc -salt -in mensagem.txt -out arquivo_criptografado -pass file:chave_sessao.bin
```

O OpenSSL apresentou o seguinte aviso:

```text id="s7k2pl"
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Após a criptografia, os arquivos presentes foram:

```bash id="6h1v8s"
ls
```

Saída:

```text id="q4c8zt"
arquivo_criptografado  chave_compartilhada.bin  chave_privada.pem  chave_publica.pem  chave_sessao.bin  mensagem.txt
```

O arquivo `arquivo_criptografado` contém a versão cifrada da mensagem.

---

## 7. Recuperação da mensagem

Para recuperar o conteúdo original, foi utilizada a mesma chave de sessão empregada na criptografia:

```bash id="m5r2yp"
openssl enc -d -aes-256-cbc -in arquivo_criptografado -out mensagem_recuperada.txt -pass file:chave_sessao.bin
```

O OpenSSL apresentou novamente o aviso relacionado à derivação de chave:

```text id="x6p9wk"
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Em seguida, foi utilizado `ls` para verificar os arquivos:

```bash id="b3q7vn"
ls
```

Saída:

```text id="z2f8mc"
arquivo_criptografado    chave_privada.pem  chave_sessao.bin         mensagem.txt
chave_compartilhada.bin  chave_publica.pem  mensagem_recuperada.txt
```

### Evidência solicitada

O **passo 6** é o registro solicitado para a atividade, demonstrando a recuperação da mensagem:

```text id="u8j1xr"
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl enc -d -aes-256-cbc -in arquivo_criptografado -out mensagem_recuperada.txt -pass file:chave_sessao.bin
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
arquivo_criptografado    chave_privada.pem  chave_sessao.bin         mensagem.txt
chave_compartilhada.bin  chave_publica.pem  mensagem_recuperada.txt
```

[**Evidências — Módulo 8 / Aulas 31 e 32**](../evidencias.pdf)

---

## 8. Verificação do conteúdo recuperado

Para confirmar a recuperação da mensagem, foi utilizado:

```bash id="r9c4yx"
cat mensagem_recuperada.txt
```

Saída:

```text id="v5q2ka"
Hackers do bem!
```

O conteúdo recuperado corresponde à mensagem original.

---

## Observação técnica sobre o roteiro

Existe uma particularidade importante nos comandos fornecidos nesta atividade.

O exercício gera:

```text id="f2w6md"
chave_compartilhada.bin
```

por meio da operação:

```bash id="k3n8pz"
openssl pkeyutl -derive -inkey chave_privada.pem -peerkey chave_publica.pem -out chave_compartilhada.bin
```

Porém, o comando utilizado posteriormente para o AES é:

```bash id="y4t1cs"
-pass file:chave_sessao.bin
```

Ou seja, **a chave compartilhada derivada por ECC não é efetivamente utilizada pelo comando AES da atividade**. A criptografia utiliza diretamente `chave_sessao.bin`, que foi gerada aleatoriamente com `openssl rand`.

Portanto, os comandos demonstram separadamente a derivação ECC e a criptografia simétrica, mas não implementam completamente um fluxo híbrido ECC → chave compartilhada → AES como a descrição conceitual pode sugerir.

Em uma implementação real, seria necessário utilizar corretamente a saída da derivação, aplicar uma KDF apropriada e então utilizar a chave resultante para a criptografia simétrica. Também é recomendável utilizar mecanismos de criptografia autenticada e evitar construções legadas de derivação de chave.

---

## Aviso do OpenSSL

O comando AES utilizado pelo laboratório apresentou:

```text id="b0f3xr"
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

O aviso indica que a forma de derivação de chave utilizada pelo comando é considerada legada. Em aplicações atuais, deve-se preferir uma derivação baseada em **PBKDF2** ou outro KDF adequado, conforme o caso.

---

## Resultado

A atividade demonstrou a geração de um par de chaves ECC utilizando `prime256v1`, a realização de uma operação de derivação e a utilização de AES-256-CBC para proteger a mensagem.

Após a descriptografia, o conteúdo recuperado foi:

```text id="e3w7pk"
Hackers do bem!
```

Assim, foi possível confirmar que o arquivo criptografado pôde ser recuperado corretamente utilizando a chave de sessão empregada no processo.
