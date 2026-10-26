# Activity 8.01 — Using Steganography on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 29–30  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use steganography to hide the contents of a text file inside a JPG image and then recover the hidden file from the image.

For this purpose, `steghide` was used, a tool capable of embedding data in cover files such as images and audio files.

## Environment

- **Operating system:** Kali Linux
- **Tool:** Steghide
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **Text file:** `mensagem.txt`
- **Cover file:** `Marcel_Proust_1895-cropped.jpg`

> Credentials and passwords used in the lab environment are not recorded in this README.

## 1. Switching to the Root User

First, the terminal was opened and administrative access was obtained:

```bash
sudo -i
```

## 2. Creating the Working Directory

The `Arquivos` directory was created inside `Documentos`:

```bash
mkdir -m 777 /home/aluno/Documentos/Arquivos
```

The directory was then accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

## 3. Creating the Message

The `mensagem.txt` file was created:

```bash
nano mensagem.txt
```

The following content was entered:

```text
Hackers do bem com Esteganografia!
```

This file would be used as the hidden content embedded in the image.

## 4. Downloading the Image

A JPG image hosted on Wikimedia was used:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/1/1b/Marcel_Proust_1895-cropped.jpg
```

Output recorded during the lab:

```text
--2024-03-03 20:07:52--  https://upload.wikimedia.org/wikipedia/commons/1/1b/Marcel_Proust_1895-cropped.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 657966 (643K) [image/jpeg]
Salvando em: “Marcel_Proust_1895-cropped.jpg”

Marcel_Proust_1895-cropped.jpg 100%[===================================================>] 642,54K  --.-KB/s    em 0,1s    

2024-03-03 20:07:52 (4,62 MB/s) - “Marcel_Proust_1895-cropped.jpg” salvo [657966/657966]
```

## 5. Verifying the Files

The `ls` command was used to confirm that both the image and the text file were present:

```bash
ls
```

Output:

```text
Marcel_Proust_1895-cropped.jpg  mensagem.txt
```

At this point, both files required for the activity were available in the directory.

## 6. Hiding the Message in the Image

`steghide` was used to embed `mensagem.txt` inside the image:

```bash
steghide embed -cf Marcel_Proust_1895-cropped.jpg -ef mensagem.txt
```

During execution, a passphrase was requested to protect the embedded content.

Output:

```text
Enter passphrase: 
Re-Enter passphrase: 
embedding "mensagem.txt" in "Marcel_Proust_1895-cropped.jpg"... done
```

The command uses the following parameters:

- `embed` — indicates that data will be embedded in the cover file.
- `-cf` — *cover file*, the file used to conceal the data.
- `-ef` — *embed file*, the file to be embedded in the image.

After the operation, `Marcel_Proust_1895-cropped.jpg` contained the hidden data.

## 7. Removing the Original File

To demonstrate that the message could later be recovered from the image, the original `mensagem.txt` file was deleted:

```bash
rm mensagem.txt
```

The directory contents were then checked:

```bash
ls
```

Output:

```text
Marcel_Proust_1895-cropped.jpg
```

At this point, the original text file was no longer present in the directory. The only remaining copy of the message was embedded in the image.

## 8. Extracting the Hidden Message

To recover the hidden content, the following command was used:

```bash
steghide extract -sf Marcel_Proust_1895-cropped.jpg
```

The passphrase used during the embedding process was requested.

Output:

```text
Enter passphrase: 
wrote extracted data to "mensagem.txt".
```

The parameter used was:

- `-sf` — *stego file*, the file containing the hidden data.

`steghide` identified the data embedded in the image and recreated the `mensagem.txt` file.

## 9. Verifying the Recovered Message

After extraction, the directory contents were checked:

```bash
ls
```

Output:

```text
Marcel_Proust_1895-cropped.jpg  mensagem.txt
```

The contents of the recovered file were then displayed:

```bash
cat mensagem.txt
```

Output:

```text
Hackers do bem com Esteganografia!
```

The original message was successfully recovered from the image, demonstrating how the steganography technique used in the lab works.

## Evidence

The evidence requested for this activity corresponds to step 9, showing the presence of `mensagem.txt` after extraction and the recovered content.

Evidence for this activity is included in the PDF for Module 8, Classes 29–30.

[View Evidence — Classes 29–30](../evidencias.pdf)

---

[Back to Classes 29–30](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
