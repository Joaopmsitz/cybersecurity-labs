# Activity 10.2 - Windows Memory Dump with FTK Imager

## Overview

This activity demonstrates volatile memory acquisition on a Windows system using AccessData FTK Imager.

The training environment uses the `forensewin` virtual machine, where FTK Imager is already installed.

## Objectives

- Open FTK Imager.
- Access the Capture Memory function.
- Configure the destination path and output filename.
- Generate a Windows memory image.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forensewin` |
| Operating System | Windows |
| Memory Acquisition Tool | FTK Imager |
| Destination Directory | `C:\Users\aluno\Documents` |
| Output File | `memdump.mem` |

## Procedure

### 1. Open FTK Imager

Log in to the supplied Windows laboratory machine and start FTK Imager.

### 2. Open the Memory Capture Dialog

In FTK Imager:

1. Open **File**.
2. Select **Capture Memory**.

Alternatively, use the corresponding toolbar button.

### 3. Configure the Memory Capture

Set the destination directory:

```text
C:\Users\aluno\Documents
```

Set the output filename:

```text
memdump.mem
```

Leave the virtual memory inclusion option unchecked, as instructed by the course.

Leave the vendor-specific output format option unchecked for this exercise.

### 4. Start the Acquisition

Select **Capture Memory**.

Wait for the acquisition process to complete.

### 5. Clean Up the Lab File

After the activity and any required validation are complete, remove the large memory image from the laboratory workstation to release storage space.

## Expected Result

FTK Imager creates the Windows memory image `memdump.mem` in the configured Documents directory.

## Evidence

No screenshot is required for Activity 10.2 in the course's final evidence PDF.

## Technical Notes

- Memory acquisition captures volatile information that may disappear when the system is powered off.
- The laboratory stores the dump locally for instructional purposes.
- Real forensic investigations should use a separate external destination to reduce changes to the system under examination.
- Record the acquisition context, system details, tool version, destination, and integrity hashes according to the applicable forensic procedure.
- Treat memory images as sensitive evidence because they may contain credentials, tokens, and private data.

## References

- [Exterro - FTK Imager User Guide](https://d1kpmuwb7gvu1i.cloudfront.net/Imager/8.2/Exterro%20FTK%20Imager%208.2%20-%20User%20Guide-%20.pdf)

## Navigation

- [Class 10](../README.md)
- [Previous Activity - 10.1](../atividade-10.1-dump-memoria-linux/README.md)
- [Next Activity - 10.3](../atividade-10.3-evidencias-logicas-memoria/README.md)
