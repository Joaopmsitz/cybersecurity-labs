# Activity 8.06 — Computing MD5, RIPEMD-160, and BLAKE2 Hashes

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 31–32  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Calculate the **hash** of a file using different cryptographic hash algorithms on Kali Linux:

- MD5
- RIPEMD-160
- BLAKE2

This activity compares the different digest lengths and demonstrates how each algorithm produces a hexadecimal representation of a file's contents.

---

## Environment

- **Operating system:** Kali Linux
- **Tools:** `md5sum`, `openssl`, and `b2sum`
- **Working directory:** `/home/aluno/Documentos/Arquivos`
- **File analyzed:** `mensagem.txt`
- **Content:** `Hackers do bem!`

> Credentials used to access the lab environment are not recorded in this README.

---

## 1. Switching to the Root User

Administrative access to Kali Linux was obtained:

```bash
sudo -i
```

---

## 2. Accessing the Working Directory

The `Arquivos` directory was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The text file was then created:

```bash
nano mensagem.txt
```

The following content was entered:

```text
Hackers do bem!
```

---

## 3. Verifying the File

After creating the file, `ls` was used to verify its presence:

```bash
ls
```

Output:

```text
mensagem.txt
```

The `mensagem.txt` file became the input used for calculating the different hashes.

---

## 4. Calculating the MD5 Hash

The `md5sum` command was used:

```bash
md5sum mensagem.txt
```

Output:

```text
ac640793b0fe42e14c071f53fe8f8486  mensagem.txt
```

The result contains **32 hexadecimal characters**, corresponding to 128 bits.

The `md5sum` command calculates the MD5 digest of the file's contents and displays the result alongside the processed filename.

---

## 5. Calculating the RIPEMD-160 Hash

OpenSSL was then used to calculate the RIPEMD-160 hash:

```bash
openssl dgst -ripemd160 mensagem.txt
```

Output:

```text
RIPEMD-160(mensagem.txt)= 1ec06a94e04fc961bad8957e1fd1f27af9dd421d
```

The result contains **40 hexadecimal characters**, corresponding to 160 bits.

The `openssl dgst` command calculates a cryptographic digest using the specified algorithm, in this case, `-ripemd160`.

---

## 6. Calculating the BLAKE2 Hash

Finally, `b2sum` was used to calculate the BLAKE2 hash:

```bash
b2sum mensagem.txt
```

Output:

```text
a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98  mensagem.txt
```

The result contains **128 hexadecimal characters**, corresponding to 512 bits.

---

## 7. Evidence — BLAKE2

The evidence requested for this activity corresponds to **step 7**, in which the BLAKE2 hash of `mensagem.txt` is calculated:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# b2sum mensagem.txt 
a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98  mensagem.txt
```

[View Evidence — Classes 31–32](../evidencias.pdf)

---

## Comparison of Results

| Algorithm | Digest Length | Computed Hash |
|---|---:|---|
| MD5 | 128 bits | `ac640793b0fe42e14c071f53fe8f8486` |
| RIPEMD-160 | 160 bits | `1ec06a94e04fc961bad8957e1fd1f27af9dd421d` |
| BLAKE2b | 512 bits | `a7158864d19a20e26c1bf13b1a802b73614932d52cea5282e8b0bbc6b6520f322510b1e747a1514429b42a405dc8403c845382859a2b59e34784c736effc3c98` |

All three algorithms produced different digests for the same file, with different output lengths.

**MD5** and **RIPEMD-160** are historical algorithms and should not be selected for new applications that require modern collision resistance. The **BLAKE2** family was designed later and offers variants with different output lengths. In this activity, `b2sum` produces a 512-bit digest using BLAKE2b by default.

---

## Result

This activity demonstrated how to calculate different hash functions for the same file using tools available on Kali Linux.

The resulting values can be used to check whether a file's contents have changed: any modification to the content will generally produce a different digest.

---

[Back to Classes 31–32](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
