# Activity 1.1 — Comparing Text Files to Detect Changes

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 01–02  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Verify whether a text file has changed by comparing an original file with a copy. This activity uses the Linux `diff` command to identify differences after modifying the copied file.

## Environment

- **Operating system:** Kali Linux
- **User account:** `aluno`, with a superuser shell used during the activity
- **Working directory:** `/home/aluno/Documentos`
- **Tools:** `diff`, `cp`, `ls`, and `nano`

## Procedure

### 1. Create the Original Text File

A text file named `Texto.txt` was created using the Kali Linux text editor.

The file contained the following text:

```text
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum. Aliquam nonummy auctor massa. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nulla at risus. Quisque purus magna, auctor et, sagittis ac, posuere eu, lectus. Nam mattis, felis ut adipiscing.
```

The file was saved in:

```bash
/home/aluno/Documentos/
```

### 2. Open a Superuser Shell

The terminal was opened and the following command was executed:

```bash
sudo -i
```

After authentication, the terminal session switched to the `root` user.

**Note:** Elevated privileges are generally unnecessary for comparing files in a directory the current user can access. Following the principle of least privilege is preferable during routine file operations.

### 3. Navigate to the Working Directory

The directory containing the original file was accessed:

```bash
cd /home/aluno/Documentos/
```

The `ls` command was used to list the files:

```bash
ls
```

The file `Texto.txt` was confirmed to be present.

### 4. Create a Copy of the File

The original file was copied using `cp`:

```bash
cp Texto.txt Texto_copia.txt
```

The directory contents were checked again:

```bash
ls
```

Both files were present:

```text
Texto.txt
Texto_copia.txt
```

### 5. Compare the Files Before Modification

The `diff` command was executed:

```bash
diff Texto.txt Texto_copia.txt
```

No output was displayed, indicating that the two files had identical contents at the time of comparison.

### 6. Modify the Copy

The copied file was opened in the `nano` editor:

```bash
nano Texto_copia.txt
```

The first letter `L` in the text was changed to `P`.

Original text:

```text
Lorem ipsum dolor sit amet...
```

Modified text:

```text
Porem ipsum dolor sit amet...
```

The modified file was saved and the editor was closed.

### 7. Compare the Files Again

The comparison was repeated:

```bash
diff Texto.txt Texto_copia.txt
```

This time, `diff` reported a difference in the first line. The relevant output was:

```diff
1c1
< Lorem ipsum dolor sit amet...
---
> Porem ipsum dolor sit amet...
```

The output above is abbreviated to highlight the change; the actual output included the complete line.

## Interpreting the Results

The `diff` command compares file contents and displays the differences it finds.

- `1c1` indicates that line 1 in the first file differs from line 1 in the second file. The letter `c` means *change*.
- `<` identifies the line from the original file, `Texto.txt`.
- `---` separates the original content from the modified content.
- `>` identifies the line from the copied file, `Texto_copia.txt`.

The comparison identified the change from `Lorem` to `Porem`, demonstrating that a modification made after copying a file can be detected through direct content comparison.

## Commands Used

```bash
sudo -i
cd /home/aluno/Documentos/
ls
cp Texto.txt Texto_copia.txt
ls
diff Texto.txt Texto_copia.txt
nano Texto_copia.txt
diff Texto.txt Texto_copia.txt
```

## Result

The activity demonstrated how to compare a text file with its copy and identify content changes.

The first comparison produced no output because the files were identical. After the copy was modified, the second comparison identified the changed line.

## Concepts Practiced

- File integrity and change detection
- Text file comparison
- Linux command-line operations
- File copying and editing
- `diff`, `cp`, `ls`, and `nano`
- Interpretation of command output

**Technical distinction:** `diff` identifies differences in file content. Cryptographic hashes, such as SHA-256, can provide a separate method for checking whether file contents have changed.

## Evidence

The visual evidence requested for the activity is included in the PDF for Classes 01–02.

The relevant screenshot shows the `diff` command after `Texto_copia.txt` was modified, demonstrating the difference between the original file and its copy.

[View Evidence — Classes 01–02](../evidencias.pdf)

---

[Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
