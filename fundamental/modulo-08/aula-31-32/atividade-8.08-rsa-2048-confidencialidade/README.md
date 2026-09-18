# Atividade 8.8 — RSA-2048 para Confidencialidade

## Objetivo

Utilizar o algoritmo **RSA-2048** para demonstrar um processo de criptografia assimétrica, utilizando:

* uma **chave privada**;
* uma **chave pública**;
* a chave pública para criptografar uma mensagem;
* a chave privada para recuperar a mensagem original.

A atividade demonstra o princípio de **confidencialidade** da criptografia assimétrica: o conteúdo criptografado com a chave pública pode ser recuperado utilizando a chave privada correspondente.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo:** RSA
* **Tamanho da chave:** 2048 bits
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `mensagem.txt`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash
sudo -i
```

---

## 2. Acesso ao diretório e verificação do arquivo

Foi acessado o diretório utilizado para os arquivos da atividade:

```bash
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi verificada a presença do arquivo que seria criptografado:

```bash
ls
```

Saída:

```text
mensagem.txt
```

---

## 3. Geração da chave privada RSA

Foi gerada uma chave privada utilizando o algoritmo RSA:

```bash
openssl genpkey -algorithm RSA -out chave_privada.pem
```

O OpenSSL realizou a geração da chave, apresentando caracteres de progresso no terminal durante o processo.

A chave privada foi armazenada no arquivo:

```text
chave_privada.pem
```

A chave privada é o componente que deve permanecer protegido e não deve ser compartilhado.

---

## 4. Geração da chave pública

A partir da chave privada, foi extraída a chave pública:

```bash
openssl rsa -pubout -in chave_privada.pem -out chave_publica.pem
```

Saída:

```text
writing RSA key
```

A estrutura de arquivos passou a ser:

```bash
ls
```

Saída:

```text
chave_privada.pem  chave_publica.pem  mensagem.txt
```

A chave pública pode ser compartilhada e será utilizada para realizar a criptografia da mensagem.

---

## 5. Criptografia da mensagem

A mensagem foi criptografada utilizando a chave pública:

```bash
openssl pkeyutl -encrypt -pubin -inkey chave_publica.pem -in mensagem.txt -out arquivo_criptografado
```

Após a operação, foi realizada uma nova verificação:

```bash
ls
```

Saída:

```text
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem.txt
```

O arquivo `arquivo_criptografado` contém o resultado da operação de criptografia e não corresponde mais ao conteúdo legível de `mensagem.txt`.

---

## 6. Recuperação da mensagem com a chave privada

Para recuperar o conteúdo original, foi utilizada a chave privada correspondente:

```bash
openssl pkeyutl -decrypt -inkey chave_privada.pem -in arquivo_criptografado -out mensagem_recuperada.txt
```

Em seguida, foi verificada a estrutura dos arquivos:

```bash
ls
```

Saída:

```text
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem_recuperada.txt  mensagem.txt
```

### Evidência solicitada

O **passo 5 da atividade** solicita o registro da etapa de recuperação da mensagem:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl pkeyutl -decrypt -inkey chave_privada.pem -in arquivo_criptografado -out mensagem_recuperada.txt

┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem_recuperada.txt  mensagem.txt
```

[**Evidências — Módulo 8 / Aulas 31 e 32**](../evidencias.pdf)

---

## 7. Verificação da mensagem recuperada

Para confirmar que a descriptografia recuperou o conteúdo original, foi utilizado:

```bash
cat mensagem_recuperada.txt
```

Saída:

```text
Hackers do bem!
```

O conteúdo recuperado corresponde ao conteúdo da mensagem original.

---

## 8. Limpeza do ambiente

Após a conclusão do exercício, os arquivos gerados durante a atividade foram removidos:

```bash
rm arquivo_criptografado chave_privada.pem chave_publica.pem mensagem_recuperada.txt
```

A verificação final deixou apenas o arquivo original:

```bash
ls
```

Saída:

```text
mensagem.txt
```

---

## Conceito aplicado

O exercício demonstra o funcionamento básico da **criptografia assimétrica**:

```text
                CHAVE PÚBLICA
                      │
                      ▼
              ┌───────────────┐
              │   Mensagem    │
              └───────┬───────┘
                      │
                      ▼
                Criptografia
                      │
                      ▼
           arquivo_criptografado
                      │
                      │
                CHAVE PRIVADA
                      │
                      ▼
                Descriptografia
                      │
                      ▼
              mensagem original
```

A chave pública e a chave privada formam um par. Neste laboratório, a chave pública foi utilizada na criptografia e a chave privada correspondente na recuperação do conteúdo.

### Observação técnica

O exercício utiliza RSA diretamente sobre a mensagem para fins didáticos. Na prática, RSA não é normalmente utilizado para criptografar arquivos grandes diretamente devido às limitações de tamanho e desempenho. Sistemas reais costumam utilizar **criptografia híbrida**, na qual uma chave simétrica é utilizada para os dados e o RSA é utilizado para proteger essa chave. Também é comum utilizar esquemas modernos de preenchimento, como **RSA-OAEP**, em vez de depender de configurações implícitas.

---

## Resultado

Foi gerado um par de chaves RSA, utilizada a chave pública para criptografar `mensagem.txt` e, posteriormente, utilizada a chave privada correspondente para recuperar o conteúdo.

A mensagem recuperada foi:

```text
Hackers do bem!
```

Isso demonstrou, no ambiente de laboratório, o uso de RSA para proteção de confidencialidade por meio de criptografia assimétrica.
