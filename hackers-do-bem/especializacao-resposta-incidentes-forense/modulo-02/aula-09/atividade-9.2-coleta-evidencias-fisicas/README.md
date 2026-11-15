# Activity 9.2 - Collecting Physical Evidence

## Overview

This activity demonstrates physical evidence acquisition through bit-by-bit disk imaging.

The source disk is copied to a separate storage device, and the resulting image is checked using MD5 and SHA-256 hashes.

## Objectives

- Identify physical storage devices.
- Mount the external destination device.
- Calculate hashes for the source disk.
- Create a bit-by-bit disk image.
- Calculate hashes for the acquired image.
- Compare the source and image digests.

## Required Equipment

- The external Debian forensic environment prepared in Activity 9.1.
- A separate external storage device with enough capacity to store the complete disk image and hash files.

## Important Safety Warning

**This activity must be performed on the student's own physical workstation. Never perform it inside the Hackers do Bem course virtual machine.**

A wrong device selection can cause irreversible data loss.

Before acquisition:

- Identify the source disk and destination disk independently.
- Confirm the source disk is not mounted for normal use.
- Use a hardware write blocker whenever possible.
- Ensure the destination has enough free capacity.
- Never reverse the `if` and `of` parameters of the acquisition command.
- Preserve the original storage device and work with the resulting forensic image.

## Procedure

### 1. Identify Storage Devices

Inspect detected disks and partitions:

```bash
fdisk -l
```

Alternatively:

```bash
hwinfo --short --disk
```

Verify the device names and sizes before proceeding.

### 2. Mount the External Destination

The course example mounts the destination partition at `/mnt`:

```bash
mount /dev/sdc1 /mnt
```

The example assumes `/dev/sda` is the source and `/dev/sdc1` is a separate destination partition. These device names are illustrative and must be verified on the actual workstation.

### 3. Calculate Source Disk Hashes

Calculate the source disk's MD5 and SHA-256 digests:

```bash
md5sum /dev/sda | awk '{print $1}' > /mnt/sda.orig.md5
sha256sum /dev/sda | awk '{print $1}' > /mnt/sda.orig.sha256
```

The commands store only the digest value to simplify comparison.

### 4. Acquire a Bit-by-Bit Image

Create the disk image on the external destination:

```bash
dd if=/dev/sda of=/mnt/sda.dd bs=4M status=progress
```

In this command:

| Parameter | Meaning |
|---|---|
| `if=/dev/sda` | Source disk |
| `of=/mnt/sda.dd` | Output image on the external destination |
| `bs=4M` | Transfer block size |
| `status=progress` | Displays copy progress |

The output device must be different from the source device.

### 5. Calculate Image Hashes

Calculate the hashes of the acquired image:

```bash
md5sum /mnt/sda.dd | awk '{print $1}' > /mnt/sda.dd.md5
sha256sum /mnt/sda.dd | awk '{print $1}' > /mnt/sda.dd.sha256
```

### 6. Compare the Hashes

Compare the source and image MD5 values:

```bash
diff /mnt/sda.orig.md5 /mnt/sda.dd.md5
```

Compare the SHA-256 values:

```bash
diff /mnt/sda.orig.sha256 /mnt/sda.dd.sha256
```

No output means that the compared digest files contain identical values.

## Expected Result

The destination storage contains a bit-by-bit image of the source disk and its corresponding hash files.

Matching MD5 and SHA-256 values indicate that the calculated digests are identical.

## Evidence

No screenshot is required for Activity 9.2 in the course's final evidence PDF.

## Technical Notes

- `dd` reads from the input specified by `if` and writes to the output specified by `of`.
- The output image must be written to a separate destination with sufficient capacity.
- Hashes should be compared using the digest values, not filenames embedded in checksum output.
- The course's original `diff` example uses incorrect output redirection. The correct syntax is `diff file1 file2`.
- MD5 is retained because it is part of the training exercise; SHA-256 should be used as the stronger integrity digest.
- For professional acquisition workflows, use write blockers and validated forensic imaging procedures.

## References

- [GNU Coreutils - dd](https://www.gnu.org/software/coreutils/manual/coreutils.html)
- [Linux - diff manual](https://man7.org/linux/man-pages/man1/diff.1.html)

## Navigation

- [Class 09](../README.md)
- [Previous Activity - 9.1](../atividade-9.1-preparacao-ferramenta-forense/README.md)
- [Next Activity - 9.3](../atividade-9.3-analise-disco-filesystem/README.md)
