# Atividade 8.10 — RSA-2048 e Assinatura Digital

## Objetivo

Utilizar **RSA-2048** para criar e verificar uma assinatura digital utilizando o OpenSSL.

A atividade demonstra como uma assinatura digital pode ser utilizada para verificar:

* a integridade de um arquivo;
* a correspondência entre a mensagem e a assinatura;
* a autenticidade associada à posse da chave privada.

Também será realizada uma tentativa de validação utilizando uma mensagem modificada, demonstrando que a assinatura não corresponde ao conteúdo alterado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo assimétrico:** RSA
* **Tamanho da chave:** 2048 bits
* **Algoritmo de hash:** SHA-256
* **Diretório:** `/home/aluno/Documentos/Arquivos`
* **Mensagem original:** `mensagem.txt`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash id="8y2n5k"
sudo -i
```

---

## 2. Acesso ao diretório e verificação da mensagem

Foi acessado o diretório utilizado na atividade:

```bash id="4m7p2q"
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi verificada a presença da mensagem:

```bash id="r6k3vx"
ls
```

Saída:

```text id="d9w1az"
mensagem.txt
```

---

## 3. Geração da chave privada RSA-2048

Foi gerada uma chave privada RSA com 2048 bits:

```bash id="q2f8mc"
openssl genpkey -algorithm RSA -out chave_privada.pem -pkeyopt rsa_keygen_bits:2048
```

O OpenSSL apresentou caracteres de progresso durante a geração da chave.

A chave privada foi armazenada em:

```text id="u5j7bn"
chave_privada.pem
```

Essa chave deve permanecer protegida, pois é utilizada para produzir as assinaturas digitais.

---

## 4. Geração da chave pública

A chave pública correspondente foi extraída da chave privada:

```bash id="m9c4yt"
openssl rsa -pubout -in chave_privada.pem -out chave_publica.pem
```

Saída:

```text id="p7v2kx"
writing RSA key
```

A estrutura dos arquivos passou a ser:

```bash id="a1z6qw"
ls
```

Saída:

```text id="n3h8sd"
chave_privada.pem  chave_publica.pem  mensagem.txt
```

A chave pública será utilizada posteriormente para verificar a assinatura.

---

## 5. Criação da assinatura digital

A assinatura foi criada utilizando a chave privada RSA e o hash SHA-256:

```bash id="c8m2vp"
openssl dgst -sha256 -sign chave_privada.pem -out assinatura.bin mensagem.txt
```

Foi realizada uma verificação dos arquivos:

```bash id="x4q7ls"
ls
```

Saída:

```text id="k6b1rz"
assinatura.bin  chave_privada.pem  chave_publica.pem  mensagem.txt
```

O arquivo `assinatura.bin` contém a assinatura digital calculada sobre o conteúdo de `mensagem.txt`.

---

## 6. Verificação da assinatura original

A assinatura foi validada utilizando a chave pública:

```bash id="t9f3wd"
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem.txt
```

Saída:

```text id="e2v5jc"
Verified OK
```

O resultado `Verified OK` indica que a assinatura corresponde ao conteúdo atual de `mensagem.txt` e à chave pública utilizada na verificação.

---

## 7. Criação de uma mensagem modificada

Para demonstrar o comportamento da assinatura diante de uma alteração no conteúdo, foi criada uma segunda mensagem:

```bash id="s5k8mn"
nano mensagem_errada.txt
```

O conteúdo utilizado foi:

```text id="h7q1xp"
Hackers do mal!
```

Essa mensagem é diferente do conteúdo utilizado para gerar `assinatura.bin`.

---

## 8. Preparação para a verificação da mensagem alterada

A assinatura original foi mantida, enquanto a verificação passou a ser realizada utilizando `mensagem_errada.txt`.

A assinatura foi originalmente calculada sobre:

```text id="w3n6rb"
mensagem.txt
```

Enquanto a nova verificação utiliza:

```text id="v8c2qy"
mensagem_errada.txt
```

Como os conteúdos são diferentes, o resumo criptográfico utilizado na verificação também não corresponde ao resumo que originou a assinatura.

---

## 9. Verificação da assinatura utilizando a mensagem alterada

Foi realizada a tentativa de validar a assinatura original contra a mensagem modificada:

```bash id="j4m9zt"
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem_errada.txt
```

Saída:

```text id="p2x7kc"
Verification failure
4047DDE3B77F0000:error:02000068:rsa routines:ossl_rsa_verify:bad signature:../crypto/rsa/rsa_sign.c:430:
4047DDE3B77F0000:error:1C880004:Provider routines:rsa_verify:RSA lib:../providers/implementations/signature/rsa_sig.c:774
```

### Evidência solicitada

O **passo 9** é a evidência solicitada pela atividade. Ele demonstra que a assinatura gerada para a mensagem original não pode ser validada quando o conteúdo é alterado:

```text id="z6r1qb"
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem_errada.txt
Verification failure
4047DDE3B77F0000:error:02000068:rsa routines:ossl_rsa_verify:bad signature:../crypto/rsa/rsa_sign.c:430:
4047DDE3B77F0000:error:1C880004:Provider routines:rsa_verify:RSA lib:../providers/implementations/signature/rsa_sig.c:774
```

[**Evidências — Módulo 8 / Aulas 31 e 32**](../evidencias.pdf)

---

## Conceito aplicado

O processo pode ser representado da seguinte forma:

```text
                 MENSAGEM ORIGINAL
                        │
                        ▼
                    SHA-256
                        │
                        ▼
               Resumo criptográfico
                        │
                        ▼
              CHAVE PRIVADA RSA
                        │
                        ▼
                ASSINATURA DIGITAL
                        │
                        │
                        ▼
              ┌───────────────────┐
              │   Verificação     │
              │   com chave       │
              │     pública       │
              └─────────┬─────────┘
                        │
                 ┌──────┴──────┐
                 ▼             ▼
             Mensagem       Mensagem
             original       alterada
                 │             │
                 ▼             ▼
             Verified OK   Verification
                              failure
```

A assinatura digital não tem como objetivo esconder o conteúdo da mensagem. Seu objetivo é permitir a verificação de que o conteúdo apresentado corresponde ao conteúdo utilizado no processo de assinatura.

---

## Integridade e autenticidade

No primeiro teste:

```text
mensagem.txt
      +
assinatura.bin
      ↓
Verified OK
```

A assinatura corresponde à mensagem original.

Quando `mensagem_errada.txt` foi utilizada:

```text
mensagem_errada.txt
      +
assinatura.bin
      ↓
Verification failure
```

A alteração do conteúdo faz com que a verificação da assinatura falhe.

Isso demonstra a propriedade de **integridade** proporcionada pelo mecanismo de assinatura. A associação da assinatura a uma identidade também depende da proteção da chave privada e da confiança estabelecida na chave pública.

---

## Observação técnica

O comando utilizado foi:

```bash
openssl dgst -sha256 -sign chave_privada.pem -out assinatura.bin mensagem.txt
```

Assim, o processo utiliza **SHA-256** para produzir o resumo da mensagem e RSA para gerar a assinatura.

A assinatura digital é diferente da criptografia utilizada para confidencialidade: **assinar uma mensagem não a torna secreta**. Qualquer pessoa que tenha acesso ao conteúdo e à chave pública poderá verificar a assinatura.

---

## 10. Limpeza do ambiente

Após a conclusão da atividade, os arquivos gerados foram removidos:

```bash id="q8w4mf"
rm -r *
```

O terminal solicitou confirmação:

```text id="b5n7cx"
zsh: sure you want to delete all 5 files in /home/aluno/Documentos/Arquivos [yn]? y
```

Após a confirmação, foi utilizado:

```bash id="k2v9pd"
ls
```

O diretório ficou sem os arquivos utilizados na atividade.

---

## Resultado

Foi gerado um par de chaves RSA-2048 e criada uma assinatura digital SHA-256 para `mensagem.txt`.

A verificação da mensagem original retornou:

```text
Verified OK
```

Quando a mesma assinatura foi utilizada com `mensagem_errada.txt`, a verificação retornou:

```text
Verification failure
```

O resultado demonstra, na prática, que uma alteração no conteúdo da mensagem faz com que a assinatura digital deixe de ser válida.
