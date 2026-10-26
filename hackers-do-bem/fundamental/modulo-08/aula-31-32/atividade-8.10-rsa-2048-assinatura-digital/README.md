# Activity 8.10 — RSA-2048 and Digital Signatures

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 31–32  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use RSA-2048 to create and verify a digital signature with OpenSSL.

This activity demonstrates how a digital signature can be used to verify:

- The integrity of a file.
- The correspondence between a message and its signature.
- Authenticity associated with possession of the private key.

A verification attempt using a modified message is also performed to demonstrate that the original signature does not match the altered content.

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Asymmetric algorithm:** RSA
- **Key size:** 2048 bits
- **Hash algorithm:** SHA-256
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original message:** `mensagem.txt`

> Credentials used to access the lab environment are not recorded in this README.

## 1. Switching to the Root User

Administrative access to Kali Linux was obtained:

```bash
sudo -i
```

## 2. Accessing the Directory and Verifying the Message

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

## 3. Generating the RSA-2048 Private Key

An RSA private key with a size of 2048 bits was generated:

```bash
openssl genpkey -algorithm RSA -out chave_privada.pem -pkeyopt rsa_keygen_bits:2048
```

OpenSSL displayed progress characters while generating the key.

The private key was stored in:

```text
chave_privada.pem
```

This key must remain protected because it is used to produce digital signatures.

## 4. Generating the Public Key

The corresponding public key was extracted from the private key:

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

The public key will be used later to verify the signature.

## 5. Creating the Digital Signature

The signature was created using the RSA private key and SHA-256:

```bash
openssl dgst -sha256 -sign chave_privada.pem -out assinatura.bin mensagem.txt
```

The files were then checked:

```bash
ls
```

Output:

```text
assinatura.bin  chave_privada.pem  chave_publica.pem  mensagem.txt
```

The `assinatura.bin` file contains the digital signature calculated over the contents of `mensagem.txt`.

## 6. Verifying the Original Signature

The signature was verified using the public key:

```bash
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem.txt
```

Output:

```text
Verified OK
```

The `Verified OK` result indicates that the signature matches the current contents of `mensagem.txt` and the public key used for verification.

## 7. Creating a Modified Message

To demonstrate how a change in content affects signature verification, a second message was created:

```bash
nano mensagem_errada.txt
```

The following content was used:

```text
Hackers do mal!
```

This message differs from the content used to generate `assinatura.bin`.

## 8. Preparing to Verify the Modified Message

The original signature was retained, but verification would now be performed using `mensagem_errada.txt`.

The signature was originally calculated over:

```text
mensagem.txt
```

The new verification uses:

```text
mensagem_errada.txt
```

Because the contents differ, the cryptographic digest calculated during verification does not match the digest that was signed.

## 9. Verifying the Signature Against the Modified Message

An attempt was made to verify the original signature against the modified message:

```bash
openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem_errada.txt
```

Output:

```text
Verification failure
4047DDE3B77F0000:error:02000068:rsa routines:ossl_rsa_verify:bad signature:../crypto/rsa/rsa_sign.c:430:
4047DDE3B77F0000:error:1C880004:Provider routines:rsa_verify:RSA lib:../providers/implementations/signature/rsa_sig.c:774
```

### Requested Evidence

Step 9 is the evidence requested for this activity. It demonstrates that a signature generated for the original message cannot be verified when the content is modified:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# openssl dgst -sha256 -verify chave_publica.pem -signature assinatura.bin mensagem_errada.txt
Verification failure
4047DDE3B77F0000:error:02000068:rsa routines:ossl_rsa_verify:bad signature:../crypto/rsa/rsa_sign.c:430:
4047DDE3B77F0000:error:1C880004:Provider routines:rsa_verify:RSA lib:../providers/implementations/signature/rsa_sig.c:774
```

Evidence for this activity is included in the PDF for Module 8, Classes 31–32.

[View Evidence — Classes 31–32](../evidencias.pdf)

## Concept Applied

The process can be represented as follows:

```text
                 ORIGINAL MESSAGE
                        │
                        ▼
                     SHA-256
                        │
                        ▼
                 Cryptographic digest
                        │
                        ▼
                 RSA PRIVATE KEY
                        │
                        ▼
                  DIGITAL SIGNATURE
                        │
                        ▼
              ┌────────────────────┐
              │    Verification    │
              │   using the       │
              │   public key      │
              └─────────┬──────────┘
                        │
                 ┌──────┴──────┐
                 ▼             ▼
             Original       Modified
              message        message
                 │             │
                 ▼             ▼
             Verified OK   Verification
                              failure
```

The purpose of a digital signature is not to hide the message's contents. Instead, it allows verification that the presented content matches the content used during the signing process.

## Integrity and Authenticity

In the first test:

```text
mensagem.txt
      +
assinatura.bin
      ↓
Verified OK
```

The signature matches the original message.

When `mensagem_errada.txt` was used:

```text
mensagem_errada.txt
      +
assinatura.bin
      ↓
Verification failure
```

Changing the message causes signature verification to fail.

This demonstrates the integrity property provided by the signature mechanism. Associating a signature with a specific identity also depends on protecting the private key and establishing trust in the public key.

## Technical Note

The command used was:

```bash
openssl dgst -sha256 -sign chave_privada.pem -out assinatura.bin mensagem.txt
```

The process uses SHA-256 to calculate the message digest and RSA to generate the signature.

A digital signature differs from encryption used for confidentiality: signing a message does not make it secret. Anyone with access to the message and the public key can verify the signature.

## 10. Cleaning Up the Environment

After completing the activity, the generated files were removed:

```bash
rm -r *
```

The terminal requested confirmation:

```text
zsh: sure you want to delete all 5 files in /home/aluno/Documentos/Arquivos [yn]? y
```

After confirmation, the following command was used:

```bash
ls
```

The directory no longer contained the files used in the activity.

## Result

An RSA-2048 key pair was generated, and a SHA-256 digital signature was created for `mensagem.txt`.

Verification of the original message returned:

```text
Verified OK
```

When the same signature was used with `mensagem_errada.txt`, verification returned:

```text
Verification failure
```

The result demonstrates that modifying the message content causes the digital signature verification to fail.

---

[Back to Classes 31–32](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
