# Activity 8.04 — Encrypting and Decrypting a File with 3DES on Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 29–30  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use **OpenSSL** to encrypt and decrypt a file using **3DES (Triple DES)** in CFB mode, verifying the creation of the encrypted file and its subsequent recovery.

This activity also demonstrates OpenSSL's behavior when using a cryptographic algorithm considered **legacy**.

---

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Algorithm:** 3DES / DES-EDE3-CFB
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original file:** `Hyla_japonica_sep01.jpg`
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

The directory used to store the files for this activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Downloading the Image

A JPG image hosted on Wikimedia Commons was used:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/5/5a/Hyla_japonica_sep01.jpg
```

Output recorded during the lab:

```text
--2024-03-03 20:56:15--  https://upload.wikimedia.org/wikipedia/commons/5/5a/Hyla_japonica_sep01.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 2900468 (2,8M) [image/jpeg]
Salvando em: “Hyla_japonica_sep01.jpg”

Hyla_japonica_sep01.jpg        100%[===================================================>]   2,77M  12,7MB/s    em 0,2s    

2024-03-03 20:56:15 (12,7MB/s) - “Hyla_japonica_sep01.jpg” salvo [2900468/2900468]
```

The image was opened in **Thunar** to verify the file before encryption.

---

## 4. Encrypting with 3DES

The initial file listing was checked:

```bash
ls
```

Output:

```text
Hyla_japonica_sep01.jpg
```

The file was then encrypted using OpenSSL:

```bash
openssl enc -des-ede3-cfb -salt -in Hyla_japonica_sep01.jpg -out arquivo_criptografado
```

A password was requested during the operation:

```text
enter DES-EDE3-CFB encryption password:
Verifying - enter DES-EDE3-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

After encryption, the following command was executed again:

```bash
ls
```

Result:

```text
arquivo_criptografado  Hyla_japonica_sep01.jpg
```

### Parameters Used

- `enc` — invokes OpenSSL's file encryption functionality.
- `-des-ede3-cfb` — uses Triple DES (3DES), also identified as `DES-EDE3`, in CFB mode.
- `-salt` — adds a salt to the key derivation process.
- `-in Hyla_japonica_sep01.jpg` — specifies the original image as the input.
- `-out arquivo_criptografado` — specifies the encrypted output file.

OpenSSL displayed a warning about using a legacy key derivation method and recommended `-iter` or `-pbkdf2` for modern use.

---

## 5. Evidence of Encryption

The evidence requested for this activity corresponds to **step 5**, showing the original file listing, the encryption command, and confirmation that the encrypted file was created:

```text
ls
Hyla_japonica_sep01.jpg

openssl enc -des-ede3-cfb -salt -in Hyla_japonica_sep01.jpg -out arquivo_criptografado
enter DES-EDE3-CFB encryption password:
Verifying - enter DES-EDE3-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls
arquivo_criptografado  Hyla_japonica_sep01.jpg
```

[View Evidence — Classes 29–30](../evidencias.pdf)

---

## 6. Decrypting the File

After confirming that the encrypted file had been created, the original file was removed:

```bash
rm Hyla_japonica_sep01.jpg
```

The encrypted file was then decrypted:

```bash
openssl enc -des-ede3-cfb -d -in arquivo_criptografado -out imagem.jpg
```

The password used during encryption was requested:

```text
enter DES-EDE3-CFB decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Finally, `ls` was used to verify the recovered file:

```bash
ls
```

Output:

```text
arquivo_criptografado  imagem.jpg
```

The recovered image was opened in **Thunar** to visually verify the decryption result.

---

## Technical Note

**3DES** is a legacy cryptographic algorithm. This activity demonstrates how it works through OpenSSL, but it is not the recommended choice for new projects. More modern algorithms should be considered according to the use case and security requirements.

Additionally, the command used in the lab generates a warning about legacy key derivation. OpenSSL recommends mechanisms such as **PBKDF2** to improve this process.

---

[View Evidence — Classes 29–30](../evidencias.pdf)

---

[Back to Classes 29–30](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
