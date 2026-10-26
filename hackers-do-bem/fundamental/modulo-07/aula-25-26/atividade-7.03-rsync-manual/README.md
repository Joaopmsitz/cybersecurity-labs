# Activity 7.03 — Manual Rsync

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 25–26  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Perform a manual file copy between two directories using `rsync`, understand the command's main parameters, and verify the integrity of the copied file.

---

## 1. Preparing the Directories

The directory `/home/aluno/Documentos/` was used as the base directory for the lab.

```bash
sudo -i
cd /home/aluno/Documentos/
mkdir -m 777 PastaA PastaB
ls
```

Output:

```text
PastaA  PastaB
```

The resulting directory structure was:

```text
/home/aluno/Documentos/
├── PastaA/
└── PastaB/
```

---

## 2. Creating the Test File

The file `Teste.txt` was created inside `PastaA`:

```bash
cd PastaA
nano Teste.txt
```

Content:

```text
Teste de Pasta A para Pasta B
```

After saving the file, its presence was verified:

```bash
ls
```

Output:

```text
Teste.txt
```

The destination directory was then accessed:

```bash
cd /home/aluno/Documentos/PastaB
ls
```

At this point, `PastaB` was empty.

---

## 3. Copying the File Using Rsync

The following command was used to copy the file from `PastaA` to `PastaB`:

```bash
rsync -avz /home/aluno/Documentos/PastaA/Teste.txt /home/aluno/Documentos/PastaB
```

Output:

```text
sending incremental file list
Teste.txt

sent 140 bytes  received 35 bytes  350,00 bytes/sec
total size is 30  speedup is 0,17
```

### Parameters Used

- `rsync` — a tool used for synchronizing and transferring files.
- `-a` — archive mode, preserving attributes such as permissions, ownership, groups, and timestamps, while enabling recursive copying.
- `-v` — verbose mode, displaying information about the operation.
- `-z` — enables compression during data transfer.
- `/home/aluno/Documentos/PastaA/Teste.txt` — source file.
- `/home/aluno/Documentos/PastaB` — destination directory.

---

## 4. Verifying the Copy

After `rsync` finished running, the contents of `PastaB` were checked:

```bash
ls
```

Output:

```text
Teste.txt
```

The file contents were then checked:

```bash
cat Teste.txt
```

Result:

```text
Teste de Pasta A para Pasta B
```

The file was copied successfully, and its contents matched the original file.

---

## 5. Cleaning Up the Destination Directory

To prepare the environment for the next activity, the copied file was removed only from `PastaB`:

```bash
ls
rm *
```

The system requested confirmation:

```text
zsh: sure you want to delete the only file in /home/aluno/Documentos/PastaB [yn]? y
```

Then, the directory was checked again:

```bash
ls
```

`PastaB` was empty again.

The `Teste.txt` file in `PastaA` was retained because it would be used in the next activity.

---

## Evidence

Evidence for this activity is included in the PDF for Module 7, Classes 25–26.

[View Evidence — Classes 25–26](../evidencias.pdf)

---

[Back to Classes 25–26](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
