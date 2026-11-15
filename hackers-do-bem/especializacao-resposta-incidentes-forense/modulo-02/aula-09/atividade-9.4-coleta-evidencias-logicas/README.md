# Activity 9.4 - Collecting Logical Evidence

## Overview

This activity examines logical evidence stored in the forensic disk image. The image is mounted read-only so its files and metadata can be inspected without intentionally modifying the filesystem.

The exercise also uses Foremost to recover an embedded JPG image from a PDF file.

## Objectives

- Mount the disk image in read-only mode.
- Inspect files and directories.
- Examine file metadata.
- Extract an embedded JPG image using Foremost.
- Validate the recovered output.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Working Directory | `/home/aluno/forense` |
| Disk Image | `pendrive.dd` |
| Mount Point | `/mnt` |
| Recovery Tool | Foremost |
| Source PDF | `sec-us-networkbasedfirewallservice.pdf` |

## Procedure

### 1. Mount the Disk Image Read-Only

Move to the working directory:

```bash
cd /home/aluno/forense
```

Mount the image using a loop device in read-only mode:

```bash
mount -o loop,ro pendrive.dd /mnt
```

Inspect the mounted filesystem:

```bash
cd /mnt
ls -la
```

Read-only mounting is important during forensic examination because it helps protect the source image from accidental modification.

### 2. Inspect Files and Metadata

Examples of useful forensic commands include:

```bash
stat filename
```

```bash
fls -rF filename
```

```bash
strings filename
```

```bash
hexedit filename
```

```bash
pdfinfo filename
```

```bash
exiftool filename
```

### 3. Examine the PDF Metadata

Inspect the sample PDF:

```bash
pdfinfo sec-us-networkbasedfirewallservice.pdf
```

The course example identifies Adobe PDF Library 8.0 as the PDF producer.

### 4. Recover an Embedded JPG Image

Move to the directory containing the PDF:

```bash
cd /mnt/documentos/rede
```

Run Foremost:

```bash
foremost -T -a -t jpg sec-us-networkbasedfirewallservice.pdf -o /home/aluno/forense/recover
```

Foremost creates a timestamped output directory under the specified recovery location.

### 5. Inspect the Recovered Image

Navigate to the generated recovery directory. Replace the sample directory name with the one actually created:

```bash
cd /home/aluno/forense/recover_YYYYMMDD_HHMMSS
cd jpg
ls -la
```

The course example identifies the recovered image as:

```text
00000019.jpg
```

Open the extracted image with an image viewer to confirm that it can be rendered.

After completing the inspection, unmount the image:

```bash
umount /mnt
```

## Expected Result

The disk image is mounted read-only and its file contents and metadata can be examined.

Foremost recovers the embedded JPG image into a separate output directory.

## Evidence

**Required screenshot: Step 6 - Print 2, PDF page 2.**

The evidence must show:

- The personalized terminal prompt.
- The Foremost command applied to `sec-us-networkbasedfirewallservice.pdf`.
- The recovery output.
- The extracted image `00000019.jpg` successfully displayed.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- `mount -o loop,ro` accesses a filesystem image through a loop device in read-only mode.
- Read-only mounting is used to help preserve the analyzed image.
- Foremost performs file carving based on known file signatures.
- Recovered files should be stored separately from the source evidence.
- The timestamped recovery directory name depends on the execution time.

## References

- [Foremost - Debian Package](https://packages.debian.org/stable/foremost)
- [Linux - mount manual](https://man7.org/linux/man-pages/man8/mount.8.html)
- [The Sleuth Kit](https://github.com/sleuthkit/sleuthkit)

## Navigation

- [Class 09](../README.md)
- [Previous Activity - 9.3](../atividade-9.3-analise-disco-filesystem/README.md)
- [Next Activity - 9.5](../atividade-9.5-recuperacao-particoes-dados/README.md)
