# Activity 8.09 — ECC-256 for Confidentiality

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 31–32  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use Elliptic Curve Cryptography (ECC) to demonstrate a process for protecting and recovering a message.

This activity uses:

- ECC with the `prime256v1` curve.
- A private key.
- A public key.
- Shared secret derivation.
- AES-256-CBC to encrypt the message.
- Recovery of the original content using the session key.

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **ECC curve:** `prime256v1`
- **Symmetric encryption:** AES-256-CBC
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original file:** `mensagem.txt`

> Credentials used to access the lab environment are not recorded in this README.

## 1. Switching to the Root User

Administrative access to Kali Linux was obtained:

```bash
sudo -i
```

## 2. Accessing the Directory and Checking the Message

The directory used for this activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The presence of the message file was then verified:

```bash
ls
```

Output:

```text
mensagem.txt
```

The `mensagem.txt` file was used as the input for the encryption process.

## 3. Generating the ECC Private Key

A private key was generated using the `prime256v1` elliptic curve:

```bash
openssl ecparam -name prime256v1 -genkey -noout -out chave_privada.pem
```

The private key was stored in:

```text
chave_privada.pem
```

This key must be kept secure and must not be shared.

## 4. Generating the Public Key

The corresponding public key was derived from the private key:

```bash
openssl ec -in chave_privada.pem -pubout -out chave_publica.pem
```

Output:

```text
read EC key
writing EC key
```

The resulting file structure was:

```bash
ls
```

Output:

```text
chave_privada.pem  chave_publica.pem  mensagem.txt
```

The public key can be shared, while the private key must remain protected.

## 5. Generating the Keys Used for Encryption

First, a random 32-byte session key was generated:

```bash
openssl rand -out chave_sessao.bin 32
```

Next, a key derivation operation was performed using the ECC keys:

```bash
openssl pkeyutl -derive -inkey chave_privada.pem -peerkey chave_publica.pem -out chave_compartilhada.bin
```

The generated files were checked using:

```bash
ls
```

Output:

```text
chave_compartilhada.bin chave_privada.pem chave_publica.pem chave_sessao.bin mensagem.txt
```

At this point, two key-related files had been created:

- `chave_sessao.bin` — a random 32-byte session key.
- `chave_compartilhada.bin` — the result of the ECC key derivation operation.

## 6. Encrypting the Message with AES-256-CBC

The message was encrypted using AES-256-CBC:

```bash
openssl enc -aes-256-cbc -salt -in mensagem.txt -out arquivo_criptografado -pass file:chave_sessao.bin
```

OpenSSL displayed the following warning:

```text
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

After encryption, the files in the directory were checked:

```bash
ls
```

Output:

```text
arquivo_criptografado  chave_compartilhada.bin  chave_privada.pem  chave_publica.pem  chave_sessao.bin  mensagem.txt
```

The `arquivo_criptografado` file contains the encrypted version of the message.

## 7. Recovering the Message

To recover the original content, the same session key used for encryption was supplied:

```bash
openssl enc -d -aes-256-cbc -in arquivo_criptografado -out mensagem_recuperada.txt -pass file:chave_sessao.bin
```

OpenSSL displayed the key derivation warning again:

```text
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

The files were then checked using `ls`:

```bash
ls
```

Output:

```text
arquivo_criptografado    chave_privada.pem  chave_sessao.bin         mensagem.txt
chave_compartilhada.bin  chave_publica.pem  mensagem_recuperada.txt
```

### Requested Evidence

The original activity identifies step 6 as the evidence step, documenting message recovery:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl enc -d -aes-256-cbc -in arquivo_criptografado -out mensagem_recuperada.txt -pass file:chave_sessao.bin
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
arquivo_criptografado    chave_privada.pem  chave_sessao.bin         mensagem.txt
chave_compartilhada.bin  chave_publica.pem  mensagem_recuperada.txt
```

Evidence for this activity is included in the PDF for Module 8, Classes 31–32.

[View Evidence — Classes 31–32](../evidencias.pdf)

## 8. Verifying the Recovered Content

To confirm that the message was recovered, the following command was used:

```bash
cat mensagem_recuperada.txt
```

Output:

```text
Hackers do bem!
```

The recovered content matches the original message.

## Technical Note on the Procedure

There is an important detail in the commands provided for this activity.

The exercise generates:

```text
chave_compartilhada.bin
```

using the following operation:

```bash
openssl pkeyutl -derive -inkey chave_privada.pem -peerkey chave_publica.pem -out chave_compartilhada.bin
```

However, the subsequent AES command uses:

```bash
-pass file:chave_sessao.bin
```

This means that the ECC-derived shared secret is **not actually used** by the AES command. The encryption instead uses `chave_sessao.bin` directly, which was generated randomly with `openssl rand`.

Therefore, the commands demonstrate ECC key derivation and symmetric encryption separately, but they do not fully implement the hybrid ECC → shared secret → AES workflow that the conceptual description might suggest.

In a real implementation, the output of the derivation operation would need to be used correctly, passed through an appropriate key derivation function (KDF), and then used to derive the key for symmetric encryption. Authenticated encryption mechanisms are also recommended, and legacy key derivation constructions should be avoided.

## OpenSSL Warning

The AES command used in the lab displayed the following warning:

```text
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

The warning indicates that the key derivation method used by the command is considered legacy. Modern applications should prefer a derivation method based on PBKDF2 or another suitable KDF, depending on the use case.

## Result

The activity demonstrated the generation of an ECC key pair using `prime256v1`, a key derivation operation, and the use of AES-256-CBC to protect a message.

After decryption, the recovered content was:

```text
Hackers do bem!
```

This confirmed that the encrypted file could be recovered using the session key supplied during the process.

---

[Back to Classes 31–32](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
