# Activity 11.5 - Steganography with Steghide

## Overview

This activity uses Steghide to extract hidden data from a JPEG image.

The training exercise processes the supplied `fun.jpg` image and recovers an embedded text file named `festa.txt`.

## Objectives

- Inspect a steganographic image.
- Extract embedded content using Steghide.
- Review the extracted text file.
- Document the recovered information.

## Environment

| Component | Description |
|---|---|
| Steganography Tool | Steghide |
| Cover Image | `fun.jpg` |
| Extracted File | `festa.txt` |
| Input Format | JPEG |

## Procedure

### 1. Extract the Embedded File

Run the command supplied by the course:

```bash
steghide --extract -sf fun.jpg
```

Steghide requests the passphrase used to protect the embedded data, if one was configured.

After successful extraction, the embedded file is written to the current directory using its stored filename unless an alternative output name is specified.

### 2. Read the Extracted Content

Display the recovered text file:

```bash
cat festa.txt
```

Review the information contained in the extracted file.

## Expected Result

Steghide successfully extracts the hidden content from `fun.jpg` and creates the file `festa.txt`.

The contents of the recovered file can then be inspected using `cat`.

## Evidence

**Required screenshot: Print 5 - PDF page 5.**

The terminal screenshot must show:

- The personalized terminal prompt.
- The execution of `steghide --extract -sf fun.jpg`.
- The successful extraction message.
- The command `cat festa.txt` and the contents of the recovered text file.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Steghide extracts embedded data from supported cover-file formats, including JPEG.
- The `-sf` option identifies the steganographic file.
- The extraction process may request a passphrase.
- When no output filename is supplied, Steghide uses the embedded filename.
- Extracted files should be preserved as separate evidence and analyzed before being opened or executed.
- Do not publish confidential content recovered from an image.

## References

- [Steghide - Official Manual](https://steghide.sourceforge.net/documentation/manual.pdf)
- [Steghide - Kali Linux Tools](https://www.kali.org/tools/steghide/)

## Navigation

- [Class 01 - Aula 11](../README.md)
- [Previous Activity - 11.4](../atividade-11.4-senha-arquivo-zip-fcrackzip/README.md)
- [Module 03](../../README.md)
