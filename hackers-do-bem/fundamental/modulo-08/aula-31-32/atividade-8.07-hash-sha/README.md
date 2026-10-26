# Activity 8.07 — Computing SHA-1, SHA-2, and SHA-3 Hashes

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 08  
> **Classes:** 31–32  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Calculate the **hash** of a file using different algorithms from the SHA family on Kali Linux:

- SHA-1
- 512-bit SHA-2
- 512-bit SHA-3

This activity demonstrates the use of different tools to generate cryptographic digests and compares the lengths and values produced by the algorithms.

---

## Environment

- **Operating system:** Kali Linux
- **Tools:** `sha1sum`, `sha512sum`, and `sha3sum`
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

## 2. Accessing the Directory and Verifying the File

The directory used for this activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The presence of `mensagem.txt` was then verified:

```bash
ls
```

Output:

```text
mensagem.txt
```

The same file used in the previous activity was used to calculate hashes from the SHA family.

---

## 3. Calculating the SHA-1 Hash

The `sha1sum` command was used:

```bash
sha1sum mensagem.txt
```

Output:

```text
287f168af5acf44b3b06a07fb6f3a4e882a9baab  mensagem.txt
```

SHA-1 produces a **160-bit** digest represented by **40 hexadecimal characters**.

Although it is still found in legacy tools and systems, SHA-1 is not recommended for new use cases that require collision resistance.

---

## 4. Calculating the 512-bit SHA-2 Hash

To calculate the 512-bit SHA-2 hash, the following command was used:

```bash
sha512sum mensagem.txt
```

Output:

```text
d0774282912bf4b5479165a9b316f23fea1f9ae3f620f400618813347a13c8d1e297fb51196def065dafe0aa21239d719f51a8cf58410bac22fc4b40b29efeab  mensagem.txt
```

SHA-512 produces a **512-bit** digest represented by **128 hexadecimal characters**.

---

## 5. Calculating the 512-bit SHA-3 Hash

Finally, `sha3sum` was used to calculate the 512-bit SHA-3 hash:

```bash
sha3sum -b -a 512 mensagem.txt
```

Output:

```text
07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1 *mensagem.txt
```

In this command:

- `-b` specifies binary mode.
- `-a 512` selects the SHA-3 variant with a 512-bit output.

The result contains **128 hexadecimal characters**, corresponding to 512 bits.

### Requested Evidence

The evidence for this activity corresponds to **step 5**, which calculates the 512-bit SHA-3 hash:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# sha3sum -b -a 512 mensagem.txt                    
07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1 *mensagem.txt
```

[View Evidence — Classes 31–32](../evidencias.pdf)

---

## Comparison of Results

| Algorithm | Digest Length | Computed Hash |
|---|---:|---|
| SHA-1 | 160 bits | `287f168af5acf44b3b06a07fb6f3a4e882a9baab` |
| SHA-2 / SHA-512 | 512 bits | `d0774282912bf4b5479165a9b316f23fea1f9ae3f620f400618813347a13c8d1e297fb51196def065dafe0aa21239d719f51a8cf58410bac22fc4b40b29efeab` |
| SHA-3 / SHA3-512 | 512 bits | `07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1` |

All three algorithms produced distinct digests for the same file.

SHA-1 has known limitations regarding collision resistance, whereas SHA-2 and SHA-3 belong to more modern families of cryptographic hash functions.

---

## Result

This activity demonstrated how to calculate hashes using different generations of the SHA family. The resulting values can be used to verify file integrity by comparing digests calculated at different times to identify changes in the content.

---

[Back to Classes 31–32](../) · [Back to Module 8](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
