# Activity 1.3 — Verifying File Integrity with MD5 Hashes

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 01–02  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Verify file integrity by calculating and comparing MD5 hashes for identical and modified files.

This activity uses the Linux `md5sum` command to demonstrate how file content is represented by a hash value and how modifications generally produce a different result.

## Environment

- **Operating system:** Kali Linux
- **User account:** `aluno`, with a superuser shell used during the activity
- **Working directory:** `/home/aluno/Documentos`
- **Tool:** `md5sum`

## Procedure

### 1. Open a Superuser Shell

The terminal was opened and the following command was executed:

```bash
sudo -i
```

After authentication, the terminal session switched to the `root` user.

**Note:** Root privileges are not normally required to calculate hashes for files the current user can read. Using the least privileges necessary is preferable for routine file operations.

### 2. Navigate to the Working Directory

The files from the previous activities were stored in the Documents directory.

The following command was used to access it:

```bash
cd /home/aluno/Documentos/
```

### 3. List the Available Files

The `ls` command was used to list the files:

```bash
ls
```

The files created during the previous activities were present:

```text
Imagem1.png
Imagem1_copia.png
Imagem2.png
Texto.txt
Texto_copia.txt
```

### 4. Calculate the MD5 Hashes

The `md5sum` command was used to calculate the hash of each file.

For the original image:

```bash
md5sum Imagem1.png
```

For the identical image copy:

```bash
md5sum Imagem1_copia.png
```

For the modified image:

```bash
md5sum Imagem2.png
```

For the original text file:

```bash
md5sum Texto.txt
```

For the modified text copy:

```bash
md5sum Texto_copia.txt
```

Each command returned a hexadecimal hash value followed by the corresponding filename. The exact values depend on the contents of the files and are therefore not reproduced here.

### 5. Compare the Hashes

The resulting hash values were compared to identify differences.

`Imagem1.png` and `Imagem1_copia.png` produced the same hash because the files were identical.

`Imagem2.png` produced a different hash because the image had been modified.

The same behavior was observed with the text files: `Texto.txt` and `Texto_copia.txt` produced different hashes because the copy had been modified during Activity 1.1.

## Interpreting the Results

MD5 is a hash function that produces a 128-bit digest, typically displayed as a 32-character hexadecimal value.

For this laboratory:

- Identical files produced matching MD5 hashes.
- Modified files produced different MD5 hashes.
- Comparing hash values provided a practical way to detect the changes made in the previous activities.

**Security note:** MD5 is no longer considered suitable for security-sensitive integrity verification because it is vulnerable to collision attacks. For modern applications, SHA-256 is generally preferred.

A matching hash is useful evidence that two files have the same content, but MD5 hash equality does not provide a cryptographic guarantee that the files are identical.

## Commands Used

```bash
sudo -i
cd /home/aluno/Documentos/
ls
md5sum Imagem1.png
md5sum Imagem1_copia.png
md5sum Imagem2.png
md5sum Texto.txt
md5sum Texto_copia.txt
```

## Cleanup

The original activity included the following command to remove files from the working directory:

```bash
rm *
```

**Warning:** This command can delete all non-hidden files and directories matched by `*` in the current directory. It normally does not prompt for confirmation by default.

Always verify the current directory and the files selected before using a destructive command. File cleanup is not required to perform hash comparisons.

## Result

The activity demonstrated how MD5 hashes can be calculated and compared to detect file modifications.

The identical image files produced the same hash, while the modified image and text files produced different values. This provided a practical demonstration of file integrity checking through hash comparison.

## Concepts Practiced

- File integrity verification
- Cryptographic hash functions
- MD5 hashing
- Hash value comparison
- Detection of file modifications
- Linux command-line operations
- Use of `md5sum`, `ls`, and `cd`
- Safe file management practices

## Evidence

The visual evidence requested for the course is included in the PDF for Classes 01–02.

The relevant screenshot shows the execution of the `md5sum` commands and the resulting hash values for the files used in the activity.

[View Evidence — Classes 01–02](../evidencias.pdf)

---

[Back to Classes 01–02](../) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
