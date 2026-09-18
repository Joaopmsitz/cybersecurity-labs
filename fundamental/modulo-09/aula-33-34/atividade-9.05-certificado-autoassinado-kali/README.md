# Atividade 9.5 — Criando Certificados Digitais Autoassinados no Kali Linux

## Objetivo

Criar um certificado digital autoassinado no Kali Linux utilizando o OpenSSL, realizando a geração de uma chave privada RSA, criação de uma solicitação de assinatura de certificado (CSR) e emissão do certificado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo:** RSA 2048 bits
* **Certificado:** X.509 autoassinado
* **Validade:** 365 dias

> As senhas utilizadas durante o laboratório não são registradas neste README.

---

## 1. Acesso ao diretório

Após abrir o terminal e obter privilégios administrativos, foi acessado o diretório utilizado no laboratório:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 2. Geração da chave privada

Foi gerada uma chave privada RSA de 2048 bits protegida com AES-256:

```bash
openssl genpkey -algorithm RSA -out private.key -aes256
```

O OpenSSL solicitou uma senha para proteger a chave privada.

Após a geração, foi utilizado:

```bash
ls
```

Resultado:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
private.key
```

---

## 3. Criação da solicitação de certificado

A partir da chave privada foi criada uma **Certificate Signing Request (CSR)**:

```bash
openssl req -new -key private.key -out request.csr
```

O OpenSSL solicitou as informações que seriam incorporadas à solicitação.

Foram preenchidos os seguintes campos:

```text
Country Name (2 letter code) [AU]:BR
State or Province Name (full name) [Some-State]:DF
Locality Name (eg, city) []:Brasilia
Organization Name (eg, company) [Internet Widgits Pty Ltd]:RNP
Organizational Unit Name (eg, section) []:ESR
Common Name (e.g. server FQDN or YOUR name) []:esr.rnp.br
Email Address []:a@a.com.br
```

Também foram solicitados atributos adicionais da requisição.

As informações da CSR identificam a entidade para a qual o certificado será criado.

---

## 4. Geração do certificado autoassinado

A CSR foi utilizada para gerar o certificado, sendo a própria chave privada utilizada para realizar a assinatura:

```bash
openssl x509 -req -in request.csr -signkey private.key -out certificate.crt -days 365
```

O OpenSSL solicitou novamente a senha da chave privada e confirmou a assinatura:

```text
Enter pass phrase for private.key:
Certificate request self-signature ok
subject=C = BR, ST = DF, L = Brasilia, O = RNP, OU = ESR, CN = esr.rnp.br, emailAddress = a@a.com.br
```

Em seguida, foi executado:

```bash
ls
```

Resultado:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
certificate.crt  private.key  request.csr
```

---

## Evidência — Passo 5

**Frase obrigatória antes do print:**

> **Print da atividade 9.5:** certificado digital autoassinado criado com sucesso, exibindo os arquivos `certificate.crt`, `private.key` e `request.csr`.

[**Evidências — Módulo 9 / Aulas 33 e 34**](../evidencias.pdf)

---

## Fluxo da atividade

| Etapa                      | Arquivo/Resultado |
| -------------------------- | ----------------- |
| Chave privada RSA          | `private.key`     |
| Solicitação de certificado | `request.csr`     |
| Certificado autoassinado   | `certificate.crt` |
| Validade                   | 365 dias          |

---

## Resultado

Foi criado com sucesso um certificado X.509 autoassinado a partir de uma chave RSA de 2048 bits.

O certificado `certificate.crt` foi gerado utilizando a própria `private.key` para realizar a assinatura.
