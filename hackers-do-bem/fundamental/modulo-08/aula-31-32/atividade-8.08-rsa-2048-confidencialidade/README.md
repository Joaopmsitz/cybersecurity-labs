# Activity 8.08 — RSA-2048 for Confidentiality

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 31–32  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use the RSA-2048 algorithm to demonstrate an asymmetric encryption process involving:

- A private key.
- A public key.
- The public key to encrypt a message.
- The private key to recover the original message.

This activity demonstrates the confidentiality principle of asymmetric cryptography: content encrypted with a public key can be recovered using the corresponding private key.

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Algorithm:** RSA
- **Key size:** 2048 bits
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original file:** `mensagem.txt`

> Credentials used to access the lab environment are not recorded in this README.

## 1. Switching to the Root User

Administrative access to Kali Linux was obtained:

```bash
sudo -i
```

## 2. Accessing the Directory and Verifying the File

The directory used to store the files for this activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The presence of the file to be encrypted was then verified:

```bash
ls
```

Output:

```text
mensagem.txt
```

## 3. Generating the RSA Private Key

A private key was generated using the RSA algorithm:

```bash
openssl genpkey -algorithm RSA -out chave_privada.pem
```

OpenSSL generated the key, displaying progress characters in the terminal during the process.

The private key was stored in the following file:

```text
chave_privada.pem
```

The private key must remain protected and should not be shared.

## 4. Generating the Public Key

The public key was extracted from the private key:

```bash
openssl rsa -pubout -in chave_privada.pem -out chave_publica.pem
```

Output:

```text
writing RSA key
```

The resulting file structure was:

```bash
ls
```

Output:

```text
chave_privada.pem  chave_publica.pem  mensagem.txt
```

The public key can be shared and will be used to encrypt the message.

## 5. Encrypting the Message

The message was encrypted using the public key:

```bash
openssl pkeyutl -encrypt -pubin -inkey chave_publica.pem -in mensagem.txt -out arquivo_criptografado
```

After the operation, the directory contents were checked again:

```bash
ls
```

Output:

```text
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem.txt
```

The `arquivo_criptografado` file contains the result of the encryption operation and is no longer the readable content of `mensagem.txt`.

## 6. Recovering the Message with the Private Key

To recover the original content, the corresponding private key was used:

```bash
openssl pkeyutl -decrypt -inkey chave_privada.pem -in arquivo_criptografado -out mensagem_recuperada.txt
```

The file structure was then checked:

```bash
ls
```

Output:

```text
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem_recuperada.txt  mensagem.txt
```

### Requested Evidence

Step 5 of the activity requests evidence of the message recovery process:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl pkeyutl -decrypt -inkey chave_privada.pem -in arquivo_criptografado -out mensagem_recuperada.txt

┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# ls
arquivo_criptografado  chave_privada.pem  chave_publica.pem  mensagem_recuperada.txt  mensagem.txt
```

Evidence for this activity is included in the PDF for Module 8, Classes 31–32.

[View Evidence — Classes 31–32](../evidencias.pdf)

## 7. Verifying the Recovered Message

To confirm that decryption recovered the original content, the following command was used:

```bash
cat mensagem_recuperada.txt
```

Output:

```text
Hackers do bem!
```

The recovered content matches the original message.

## 8. Cleaning Up the Environment

After completing the exercise, the files generated during the activity were removed:

```bash
rm arquivo_criptografado chave_privada.pem chave_publica.pem mensagem_recuperada.txt
```

The final check showed that only the original file remained:

```bash
ls
```

Output:

```text
mensagem.txt
```

## Concept Applied

The exercise demonstrates the basic operation of asymmetric encryption:

```text
                 PUBLIC KEY
                     │
                     ▼
             ┌───────────────┐
             │    Message    │
             └───────┬───────┘
                     │
                     ▼
                 Encryption
                     │
                     ▼
          arquivo_criptografado
                     │
                     │
                 PRIVATE KEY
                     │
                     ▼
                 Decryption
                     │
                     ▼
              Original message
```

The public and private keys form a pair. In this lab, the public key was used for encryption, and the corresponding private key was used to recover the content.

## Technical Note

This exercise uses RSA directly on the message for educational purposes. In practice, RSA is not normally used to encrypt large files directly because of message-size limitations and performance considerations.

Real-world systems typically use **hybrid encryption**, in which a symmetric key encrypts the data and RSA protects that key. Modern padding schemes such as **RSA-OAEP** are also commonly used instead of relying on implicit settings.

## Result

An RSA key pair was generated, the public key was used to encrypt `mensagem.txt`, and the corresponding private key was subsequently used to recover its contents.

The recovered message was:

```text
Hackers do bem!
```

This demonstrated, in the lab environment, how RSA can provide confidentiality through asymmetric encryption.

---

[Back to Classes 31–32](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
