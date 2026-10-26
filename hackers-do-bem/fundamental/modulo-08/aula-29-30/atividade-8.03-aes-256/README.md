# Activity 8.03 — Encrypting and Decrypting a File with AES-256 on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 29–30  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use **OpenSSL** to encrypt and decrypt a file using **AES-256 in CTR mode**, demonstrating how to protect a file and subsequently recover it using the password provided during encryption.

---

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Algorithm:** AES-256-CTR
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Original file:** `My_shoe.jpg`
- **Encrypted file:** `arquivo_criptografado`
- **Recovered file:** `My_shoe2.jpg`

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

## 3. Downloading the File Used in the Lab

A JPG image was downloaded from Wikimedia Commons to serve as the input file:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
```

Recorded output:

```text
--2024-03-03 20:42:50--  https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 1297035 (1,2M) [image/jpeg]
Salvando em: “My_shoe.jpg”

My_shoe.jpg                    100%[===================================================>]   1,24M  7,35MB/s    em 0,2s    

2024-03-03 20:42:51 (7,35 MB/s) - “My_shoe.jpg” salvo [1297035/1297035]
```

The image was opened in **Thunar** to visually confirm the file before encryption.

---

## 4. Encrypting with AES-256-CTR

First, the directory contents were checked:

```bash
ls
```

Output:

```text
arquivo_criptografado  My_shoe.jpg
```

OpenSSL was then used to encrypt the image:

```bash
openssl enc -aes-256-ctr -salt -in My_shoe.jpg -out arquivo_criptografado
```

During the process, a password was requested for encryption:

```text
enter AES-256-CTR encryption password:
Verifying - enter AES-256-CTR encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

After execution, the encrypted file was created.

### Parameters Used

- `enc` — invokes the OpenSSL file encryption and decryption command.
- `-aes-256-ctr` — uses AES with a 256-bit key in CTR mode.
- `-salt` — adds a salt to the key derivation process.
- `-in My_shoe.jpg` — specifies the original file as the input.
- `-out arquivo_criptografado` — specifies the encrypted output file.

OpenSSL also displayed a warning about **legacy key derivation**, recommending the use of `-iter` or `-pbkdf2` for modern operations.

---

## 5. Removing the Original File and Decrypting

To verify whether the file could be recovered from its encrypted version, the original file was deleted:

```bash
rm My_shoe.jpg
```

The directory was then checked to confirm that only the encrypted file remained:

```bash
ls
```

Output:

```text
arquivo_criptografado
```

The file was then decrypted using OpenSSL:

```bash
openssl enc -d -aes-256-ctr -in arquivo_criptografado -out My_shoe2.jpg
```

The password used previously was requested:

```text
enter AES-256-CTR decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Finally, `ls` was used to verify the recovered file:

```bash
ls
```

Output:

```text
arquivo_criptografado  My_shoe2.jpg
```

The presence of `My_shoe2.jpg` demonstrates that the content was recovered from the encrypted file.

The recovered image was also opened in **Thunar** to visually verify the decryption result.

---

## Evidence

The evidence requested for this activity corresponds to **step 6**, demonstrating the removal of the original file, the presence of the encrypted file, the decryption process, and the creation of the recovered image:

```text
rm My_shoe.jpg
ls
arquivo_criptografado

openssl enc -d -aes-256-ctr -in arquivo_criptografado -out My_shoe2.jpg
enter AES-256-CTR decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls
arquivo_criptografado  My_shoe2.jpg
```

[View Evidence — Classes 29–30](../evidencias.pdf)

---

[Back to Classes 29–30](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
