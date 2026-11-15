# Activity 9.3 - Analyzing the Disk and Filesystem

## Overview

This activity performs a summary examination of a forensic disk image using The Sleuth Kit and standard Linux utilities.

The provided `pendrive.dd` image represents a 1 GB USB storage device. The exercise examines its filesystem, volume metadata, sector count, and directory entries.

## Objectives

- Prepare the forensic working directory.
- Decompress the disk image.
- Verify its integrity using MD5 and SHA-256.
- Identify the filesystem type and volume information.
- Determine the number of sectors.
- List files and directories contained in the image.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Source Directory | `/curso/aula9` |
| Working Directory | `/home/aluno/forense` |
| Disk Image | `pendrive.dd` |
| Forensic Toolkit | The Sleuth Kit |

## Procedure

### 1. Prepare the Working Directory

Open a root shell:

```bash
sudo su
```

Create the forensic working directory:

```bash
cd /home/aluno
mkdir forense
cd forense
```

Copy the supplied course files:

```bash
cp /curso/aula9/* .
ls -la
```

### 2. Decompress the Disk Image

Preserve the compressed source and extract the image:

```bash
bunzip2 -k pendrive.dd.bz2
```

Verify the extracted file:

```bash
ls -la
```

### 3. Verify Image Integrity

Generate MD5 and SHA-256 hashes:

```bash
md5sum pendrive.dd | awk '{print $1}' > pendrive.dd.md5
sha256sum pendrive.dd | awk '{print $1}' > pendrive.dd.sha256
```

Extract the original reference digest values:

```bash
awk '{print $1}' pendrive.orig.md5 > pendrive.orig.md5.value
awk '{print $1}' pendrive.orig.sha256 > pendrive.orig.sha256.value
```

Compare the MD5 values:

```bash
diff pendrive.dd.md5 pendrive.orig.md5.value
```

Compare the SHA-256 values:

```bash
diff pendrive.dd.sha256 pendrive.orig.sha256.value
```

No output indicates identical digest values.

### 4. Examine the Disk and Filesystem

Identify disk and partition information:

```bash
fdisk -l pendrive.dd
```

Identify the file type:

```bash
file pendrive.dd
```

Display filesystem information:

```bash
fsstat pendrive.dd
```

List files and directories recursively:

```bash
fls -ruF pendrive.dd
```

## Expected Results

The course example identifies the following characteristics:

| Question | Expected Result |
|---|---|
| Filesystem | FAT32 |
| Volume Label | SOUZASANTOS |
| Number of Sectors | 2,007,040 |
| Disk Image Size | 1,027,604,480 bytes |

The recursive file listing includes paths such as:

- `documentos/rede/`
- `documentos/diversos/`
- `documentos/pesquisas_google/`
- `fotos/`
- `Literary Review.doc`

The exact output is determined by the supplied image and the installed Sleuth Kit version.

## Evidence

**Required screenshot: Step 7 - Print 1, PDF page 1.**

The screenshot must show the terminal under the personalized prompt and the output of the `fls` command, listing file names and directory paths recovered from `pendrive.dd`.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- `fdisk -l` reports partition and sector information.
- `file` identifies recognizable file signatures and filesystem characteristics.
- `fsstat` displays filesystem metadata and structural information.
- `fls` lists file and directory entries from the forensic image.
- The Sleuth Kit can also display deleted file entries and filesystem metadata.
- Decompression is performed on a working copy while preserving the original compressed source.

## References

- [The Sleuth Kit - fls](https://manpages.debian.org/trixie/sleuthkit/fls.1.en.html)
- [The Sleuth Kit - fsstat](https://manpages.debian.org/trixie/sleuthkit/fsstat.1.en.html)
- [The Sleuth Kit - Tool Overview](https://github.com/sleuthkit/sleuthkit/wiki/TSK_Tool_Overview)

## Navigation

- [Class 09](../README.md)
- [Previous Activity - 9.2](../atividade-9.2-coleta-evidencias-fisicas/README.md)
- [Next Activity - 9.4](../atividade-9.4-coleta-evidencias-logicas/README.md)
