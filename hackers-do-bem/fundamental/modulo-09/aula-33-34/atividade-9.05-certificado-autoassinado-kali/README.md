# Activity 9.05 — Creating Self-Signed Digital Certificates on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 33–34  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Create a self-signed digital certificate on Kali Linux using OpenSSL by generating an RSA private key, creating a Certificate Signing Request (CSR), and issuing the certificate.

---

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Algorithm:** RSA 2048-bit
- **Certificate:** Self-signed X.509
- **Validity period:** 365 days

> Passwords used during the lab are not recorded in this README.

---

## 1. Accessing the Working Directory

After opening the terminal and obtaining administrative privileges, the directory used in the lab was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 2. Generating the Private Key

An RSA private key with a size of 2048 bits was generated and protected with AES-256:

```bash
openssl genpkey -algorithm RSA -out private.key -aes256
```

OpenSSL prompted for a password to protect the private key.

After the key was generated, the following command was used:

```bash
ls
```

Output:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
private.key
```

---

## 3. Creating the Certificate Signing Request

A **Certificate Signing Request (CSR)** was created from the private key:

```bash
openssl req -new -key private.key -out request.csr
```

OpenSSL requested the information to be included in the request.

The following fields were entered:

```text
Country Name (2 letter code) [AU]:BR
State or Province Name (full name) [Some-State]:DF
Locality Name (eg, city) []:Brasilia
Organization Name (eg, company) [Internet Widgits Pty Ltd]:RNP
Organizational Unit Name (eg, section) []:ESR
Common Name (e.g. server FQDN or YOUR name) []:esr.rnp.br
Email Address []:a@a.com.br
```

Additional request attributes were also requested.

The CSR information identifies the entity for which the certificate will be created.

---

## 4. Generating the Self-Signed Certificate

The CSR was used to generate the certificate, with the same private key used to sign it:

```bash
openssl x509 -req -in request.csr -signkey private.key -out certificate.crt -days 365
```

OpenSSL requested the private key password again and confirmed the signature:

```text
Enter pass phrase for private.key:
Certificate request self-signature ok
subject=C = BR, ST = DF, L = Brasilia, O = RNP, OU = ESR, CN = esr.rnp.br, emailAddress = a@a.com.br
```

The following command was then executed:

```bash
ls
```

Output:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
certificate.crt  private.key  request.csr
```

---

## Evidence — Step 5

**Required caption before the screenshot:**

> Screenshot for Activity 9.5: the self-signed digital certificate was successfully created, showing the `certificate.crt`, `private.key`, and `request.csr` files.

[View Evidence — Classes 33–34](../evidencias.pdf)

---

## Activity Workflow

| Stage | File or Result |
|---|---|
| RSA private key | `private.key` |
| Certificate Signing Request | `request.csr` |
| Self-signed certificate | `certificate.crt` |
| Validity period | 365 days |

---

## Result

A self-signed X.509 certificate was successfully created using a 2048-bit RSA key.

The `certificate.crt` certificate was generated using `private.key` to sign the certificate.

---

[Back to Classes 33–34](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
