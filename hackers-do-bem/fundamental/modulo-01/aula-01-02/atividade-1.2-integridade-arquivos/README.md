# Activity 1.2 — Comparing Binary File Integrity

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 01–02  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Verify the integrity of binary files by comparing identical and modified files. This activity uses image files as examples and the Linux `cmp` command to detect byte-level differences.

## Environment

- **Operating system:** Kali Linux
- **User account:** `aluno`
- **Working directory:** `/home/aluno/Documentos`
- **Tools:** KolourPaint, `cmp`, `cd`, and `ls`

## Procedure

### 1. Open KolourPaint

KolourPaint was launched from the terminal using:

```bash
kolourpaint
```

### 2. Create the First Image

An image was created in KolourPaint using different colors and freehand drawings.

The image was saved in the Documents directory as:

```text
Imagem1.png
```

### 3. Create an Identical Copy

The same image was saved again without any modifications under the name:

```text
Imagem1_copia.png
```

At this point, `Imagem1.png` and `Imagem1_copia.png` were expected to contain identical data.

### 4. Modify the Image

A small change was then made to the image by adding a colored dot in KolourPaint.

The modified image was saved as:

```text
Imagem2.png
```

The three files used in the activity were:

```text
Imagem1.png
Imagem1_copia.png
Imagem2.png
```

`Imagem1.png` and `Imagem1_copia.png` were identical, while `Imagem2.png` contained the modification.

### 5. Verify the Files in the Terminal

After closing KolourPaint, the terminal was used to access the directory containing the images:

```bash
cd /home/aluno/Documentos
```

The files were listed with:

```bash
ls
```

The output included the image files created for this activity, along with files from Activity 1.1.

Example:

```text
Imagem1_copia.png
Imagem1.png
Imagem2.png
Texto_copia.txt
Texto.txt
```

### 6. Compare Identical Files

The original image was compared with its identical copy:

```bash
cmp Imagem1.png Imagem1_copia.png
```

The command produced no output, indicating that no differing bytes were found and both files had identical contents.

### 7. Compare the Modified Image

Next, the original image was compared with the modified version:

```bash
cmp Imagem1.png Imagem2.png
```

Because `Imagem2.png` had been modified, `cmp` reported a difference between the files.

An example of the output is:

```text
Imagem1.png Imagem2.png differ: byte 58, line 3
```

The byte position and line number shown here are illustrative; the actual output depends on the image data and the modification performed.

## Interpreting the Results

The `cmp` command compares two files byte by byte.

**First comparison:**

```bash
cmp Imagem1.png Imagem1_copia.png
```

No output was produced, indicating that the files were identical.

**Second comparison:**

```bash
cmp Imagem1.png Imagem2.png
```

The command reported a difference because the second image contained a modification.

When `cmp` reports a position such as `byte 58, line 3`, it identifies the byte where the difference was detected. For binary image files, the reported line number refers to newline characters in the underlying data; it does not represent a visual line in the image.

## Commands Used

```bash
kolourpaint
cd /home/aluno/Documentos
ls
cmp Imagem1.png Imagem1_copia.png
cmp Imagem1.png Imagem2.png
```

## Result

The activity demonstrated how to compare image files byte by byte to identify changes.

The comparison between `Imagem1.png` and `Imagem1_copia.png` found no differences because their contents were identical. The comparison between `Imagem1.png` and `Imagem2.png` detected a difference after the image was modified.

## Concepts Practiced

- File integrity and change detection
- Binary file comparison
- Byte-by-byte comparison
- Linux command-line operations
- Image file analysis
- Use of `cmp`, `ls`, and `cd`
- Interpretation of command output

**Technical distinction:** `cmp` directly compares file contents, whereas cryptographic hashes such as SHA-256 can be used to calculate and compare file fingerprints. Both approaches can help identify changes, but they serve different purposes.

## Evidence

The visual evidence requested for the course is included in the PDF for Classes 01–02.

The relevant screenshot shows the `cmp` command comparing `Imagem1.png` with `Imagem2.png`, demonstrating the detected difference between the files.

[View Evidence — Classes 01–02](../evidencias.pdf)

---

[Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
