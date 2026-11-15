# Activity 9.5 - Recovering Partitions and Data

## Overview

This activity investigates a damaged disk image whose partition table is unavailable. A sector-by-sector search using `fsstat` identifies possible filesystem starting offsets.

The resulting filesystem can then be mounted using the discovered byte offset.

## Objectives

- Inspect a damaged disk image.
- Identify the image sector count.
- Search for filesystem starting sectors.
- Record filesystem metadata in a results file.
- Mount a discovered filesystem read-only.
- Examine the recovered directory contents.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Working Directory | `/home/aluno/forense` |
| Disk Image | `hd_corrompido.dd` |
| Filesystem Utility | `fsstat` |
| Mount Point | `/mnt` |
| Expected Filesystem | Ext2 |

## Procedure

### 1. Unmount the Existing Mount Point

Open a root shell:

```bash
sudo su
```

Unmount `/mnt` if it is currently in use:

```bash
umount /mnt
```

Move to the forensic working directory:

```bash
cd /home/aluno/forense
```

### 2. Attempt to Mount the Damaged Image

Try mounting the image:

```bash
mount -o loop,ro hd_corrompido.dd /mnt
```

The course example reports an error because the disk image does not expose a recognizable partition table at its beginning.

### 3. Inspect the Disk Geometry

Run:

```bash
fdisk -l hd_corrompido.dd
```

The course example identifies:

| Attribute | Value |
|---|---:|
| Image Size | 32,112,128 bytes |
| Sector Size | 512 bytes |
| Total Sectors | 62,719 |

### 4. Create the Partition Search Script

Create the script:

```bash
nano /home/aluno/forense/partition_search.sh
```

Use the following code:

```sh
#!/bin/sh

echo "Teste de particao" > resultado.txt

for i in $(seq 1 62719); do
    if fsstat -o "$i" hd_corrompido.dd >> resultado.txt 2>/dev/null; then
        printf "setor = %s\n\n" "$i" >> resultado.txt
    fi
done
```

Save the file and close the editor.

The script iterates through the image sectors and records the filesystem information returned by `fsstat` for each detected filesystem offset.

### 5. Run the Search

Give the script execution permission:

```bash
chmod a+x partition_search.sh
```

Execute it:

```bash
./partition_search.sh
```

The course estimates an execution time of approximately 2 to 10 minutes for the supplied image.

Inspect the results:

```bash
cat resultado.txt
```

The sample output identifies five filesystem starting points. One of the identified offsets is sector `2048`, containing an Ext2 filesystem.

### 6. Mount the Recovered Partition

Create the mount point if necessary:

```bash
mkdir -p /mnt
```

Mount the first identified partition using its sector offset:

```bash
mount -o loop,ro,offset=$((2048*512)) hd_corrompido.dd /mnt
```

Inspect the recovered filesystem:

```bash
ls -la /mnt
```

Inspect the `aircrafts` directory from the course example:

```bash
ls -la /mnt/aircrafts/
```

After examination, unmount the partition:

```bash
umount /mnt
```

## Expected Result

The sector search identifies filesystem offsets in the damaged disk image.

The filesystem starting at sector `2048` is identified as Ext2 and can be mounted using its byte offset.

The mounted image exposes recovered directory entries, including the `aircrafts` directory.

## Evidence

**Required screenshot: Step 6 - Print 3, PDF page 3.**

The screenshot must show the terminal under the personalized prompt and the `cat resultado.txt` output, demonstrating the detected filesystem offsets, including sector `2048` and Ext2 filesystem information.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- `fsstat -o` examines filesystem information at a specified sector offset.
- The sector offset is multiplied by the sector size to obtain a byte offset.
- The example uses 512-byte sectors.
- The `loop` option allows a raw image file to be mounted as a loop device.
- The `ro` option requests read-only access.
- The search script is intended for the small supplied training image, not for scanning an entire physical disk.
- Preserve the original image and perform recovery work on a separate forensic copy.

## References

- [The Sleuth Kit - fsstat](https://manpages.debian.org/trixie/sleuthkit/fsstat.1.en.html)
- [Linux - mount manual](https://man7.org/linux/man-pages/man8/mount.8.html)
- [GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html)

## Navigation

- [Class 09](../README.md)
- [Previous Activity - 9.4](../atividade-9.4-coleta-evidencias-logicas/README.md)
- [Module 02](../../README.md)
