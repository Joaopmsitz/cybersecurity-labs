# Activity 8.05 — Encrypting and Decrypting a File with Blowfish on Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 29–30  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use **OpenSSL** to encrypt and decrypt a file using the **Blowfish** algorithm in CFB mode, verifying the creation of an encrypted file and its subsequent recovery.

This activity also demonstrates OpenSSL's behavior when working with a cryptographic algorithm considered legacy.

---

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Algorithm:** Blowfish (BF-CFB)
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original file:** `CRS-20_Dragon–Enhanced.jpg`
- **Encrypted file:** `arquivo_criptografado`
- **Recovered file:** `imagem.jpg`

> The password used during the lab is not recorded in this README.

---

## 1. Switching to the Root User

Administrative access to Kali Linux was obtained:

```bash
sudo -i
```

---

## 2. Accessing the Working Directory

The directory used in this activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Downloading the Image

A JPG image hosted on Wikimedia Commons was used:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/9/9e/CRS-20_Dragon%E2%80%93Enhanced.jpg
```

Recorded output:

```text
--2024-03-04 16:10:22--  https://upload.wikimedia.org/wikipedia/commons/9/9e/CRS-20_Dragon%E2%80%93Enhanced.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 2092509 (2,0M) [image/jpeg]
Salvando em: “CRS-20_Dragon–Enhanced.jpg”

CRS-20_Dragon–Enhanced.jpg     100%[===================================================>]   2,00M  10,6MB/s    em 0,2s    

2024-03-04 16:10:22 (10,6MB/s) - “CRS-20_Dragon–Enhanced.jpg” salvo [2092509/2092509]
```

The image was opened in **Thunar** to visually verify the file before encryption.

---

## 4. Encrypting with Blowfish

First, the directory contents were checked:

```bash
ls
```

Output:

```text
CRS-20_Dragon–Enhanced.jpg
```

OpenSSL was then used to encrypt the image:

```bash
openssl enc -bf-cfb -salt -in CRS-20_Dragon–Enhanced.jpg -out arquivo_criptografado
```

A password was requested during the operation:

```text
enter BF-CFB encryption password:
Verifying - enter BF-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

After encryption, the directory contents were checked again:

```bash
ls
```

Output:

```text
arquivo_criptografado  CRS-20_Dragon–Enhanced.jpg
```

### Parameters Used

- `enc` — invokes OpenSSL's file encryption functionality.
- `-bf-cfb` — uses the Blowfish algorithm in CFB mode.
- `-salt` — adds a salt to the key derivation process.
- `-in CRS-20_Dragon–Enhanced.jpg` — specifies the original image as the input.
- `-out arquivo_criptografado` — specifies the encrypted output file.

OpenSSL also displayed a warning indicating that the key derivation method being used is legacy and recommending `-iter` or `-pbkdf2`.

---

## 5. Evidence of Encryption

The evidence requested for this activity corresponds to **step 5**, showing the original file, the encryption command, and the creation of the encrypted file:

```text
ls
CRS-20_Dragon–Enhanced.jpg

openssl enc -bf-cfb -salt -in CRS-20_Dragon–Enhanced.jpg -out arquivo_criptografado
enter BF-CFB encryption password:
Verifying - enter BF-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls 
arquivo_criptografado  CRS-20_Dragon–Enhanced.jpg
```

[View Evidence — Classes 29–30](../evidencias.pdf)

---

## 6. Removing the Original File and Decrypting

To verify that the content could be recovered, the original file was deleted:

```bash
rm CRS-20_Dragon–Enhanced.jpg
```

The encrypted file was then used for decryption:

```bash
openssl enc -bf-cfb -d -in arquivo_criptografado -out imagem.jpg
```

The previously used password was requested:

```text
enter BF-CFB decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

After decryption, `ls` was used:

```bash
ls
```

Result:

```text
arquivo_criptografado  imagem.jpg
```

The recovered image was opened in **Thunar** to visually verify the decryption result.

---

## Technical Note

**Blowfish** is a symmetric-key encryption algorithm with a variable-length key and is now considered a legacy option for new projects. This activity demonstrates its operation through OpenSSL, but more modern algorithms and modes should be considered for current implementations.

It is also important to note that the command used in this lab does not specify a 128-bit key length; the `-bf-cfb` parameter selects Blowfish in CFB mode.

As in the previous activities, OpenSSL displayed a warning about legacy key derivation and recommended mechanisms such as **PBKDF2** for modern use.

---

[View Evidence — Classes 29–30](../evidencias.pdf)

---

[Back to Classes 29–30](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
