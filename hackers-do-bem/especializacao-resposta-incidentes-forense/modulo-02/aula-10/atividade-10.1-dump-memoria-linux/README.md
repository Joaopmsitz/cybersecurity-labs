# Activity 10.1 - Linux Memory Dump with AVML

## Overview

This activity acquires volatile memory from the `forenseLinux` virtual machine using AVML (Acquire Volatile Memory for Linux).

The memory image is stored in the laboratory environment for training purposes, and cryptographic hashes are generated to support integrity verification.

## Objectives

- Prepare a forensic working directory.
- Copy the supplied AVML binary.
- Acquire a Linux memory image.
- Generate MD5 and SHA-256 hashes.
- Inspect the generated files.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Memory Acquisition Tool | AVML |
| Source Directory | `/curso/aula10` |
| Working Directory | `/home/aluno/forense` |
| Output Image | `memoria.dump` |

## Procedure

### 1. Prepare the Working Directory

Open a root shell:

```bash
sudo su
```

Create the working directory:

```bash
mkdir /home/aluno/forense
cd /home/aluno/forense
```

Copy the supplied AVML binary:

```bash
cp /curso/aula10/avml .
```

### 2. Acquire Volatile Memory

Grant execution permission:

```bash
chmod a+x avml
```

Run AVML using the syntax supplied by the training environment:

```bash
./avml memoria.dump
```

List the generated files:

```bash
ls -la
```

The resulting memory image size depends on the amount of RAM available to the virtual machine.

### 3. Generate Cryptographic Hashes

Calculate the MD5 hash:

```bash
md5sum memoria.dump > /home/aluno/forense/memoria.dump.md5
```

Calculate the SHA-256 hash:

```bash
sha256sum memoria.dump > /home/aluno/forense/memoria.dump.sha256
```

Verify the generated files:

```bash
ls -la
```

### 4. Clean Up the Lab Directory

After the activity has been completed and the evidence has been preserved, the training instructions remove the working directory:

```bash
cd /home/aluno
rm -r forense/
```

Only perform cleanup after confirming that the memory image and hashes are no longer needed.

## Expected Result

AVML generates a volatile memory image named `memoria.dump` and the corresponding MD5 and SHA-256 hash files.

## Evidence

**Required screenshot: Step 2 - Print 1, PDF page 1.**

The terminal screenshot must show:

- The personalized terminal prompt.
- Creation of `/home/aluno/forense`.
- Copying the AVML binary from `/curso/aula10`.
- The prepared working directory before memory acquisition.

Configure the terminal prompt as required by the course:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\\u/meunome/g')"
```

Replace `meunome` with the required student alias.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- AVML stands for Acquire Volatile Memory for Linux.
- The course VM contains a supplied binary and uses `./avml memoria.dump`.
- Current upstream AVML documentation uses the `acquire` subcommand, for example `avml acquire memoria.dump`.
- Memory acquisition can alter system state and should be performed using a controlled forensic procedure.
- Real investigations should write the memory image to a separate external destination whenever possible.
- Preserve the acquired image and hash values as part of the evidence record.

## References

- [Microsoft - AVML](https://github.com/microsoft/avml)

## Navigation

- [Class 10](../README.md)
- [Module 02](../../README.md)
- [Next Activity - 10.2](../atividade-10.2-dump-memoria-windows/README.md)
