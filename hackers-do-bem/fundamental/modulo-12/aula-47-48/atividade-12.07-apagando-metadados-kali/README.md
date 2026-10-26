# Activity 12.07 — Removing Metadata on Kali Linux

In this activity, ExifTool was used to remove metadata from a JPEG image and compare the modified file with the original file automatically preserved by the tool.

> **Note:** Credentials used in the lab environment are not recorded in this document.

## Objective

- Remove metadata from an image.
- Identify the differences between the original file and the processed file.
- Use ExifTool for metadata sanitization.
- Observe which information remains after removal.

## Procedure

### 1. Accessing Kali Linux

Kali Linux was accessed via RDP using the address `192.168.98.40`.

A terminal was opened, and administrative privileges were obtained using:

```bash
sudo -i
```

### 2. Checking the Files

The directory used in the previous activity was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The existing files were listed:

```bash
ls
```

Output:

```text
contrato_08_2021.pdf  IPTCpanel.jpg
```

### 3. Removing the Metadata

The ExifTool `-all=` parameter was used to remove metadata from the image:

```bash
exiftool -all= IPTCpanel.jpg
```

Output:

```text
Warning: ICC_Profile deleted. Image colors may be affected - IPTCpanel.jpg
    1 image files updated
```

ExifTool updated the image and automatically preserved the original file as `IPTCpanel.jpg_original`.

### 4. Checking the Files

The following command was executed:

```bash
ls
```

Output:

```text
contrato_08_2021.pdf  IPTCpanel.jpg  IPTCpanel.jpg_original
```

### 5. Verifying the Image After Metadata Removal

The following command was executed:

```bash
exiftool IPTCpanel.jpg
```

Output:

```text
ExifTool Version Number         : 13.36
File Name                       : IPTCpanel.jpg
File Size                       : 51 kB
File Modification Date/Time     : 2025:12:06 19:59:37-03:00
File Access Date/Time           : 2025:12:06 19:59:37-03:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
DCT Encode Version              : 100
APP14 Flags 0                   : [14]
APP14 Flags 1                   : (none)
Color Transform                 : YCbCr
Image Width                     : 300
Image Height                    : 379
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 300x379
Megapixels                     : 0.114
```

Compared with the previous analysis, several EXIF, IPTC, XMP, and Photoshop fields were no longer displayed.

### 6. Verifying the Original File

The file preserved by ExifTool was analyzed:

```bash
exiftool IPTCpanel.jpg_original
```

The output retained the original metadata, including information such as:

```text
File Name                       : IPTCpanel.jpg_original
File Size                       : 87 kB
File Type                       : JPEG
JFIF Version                    : 1.02
Exif Byte Order                 : Big-endian (Motorola, MM)
Image Description               : IPTC CONTENT PANEL: DESCRIPTION
Orientation                     : Horizontal (normal)
X Resolution                    : 600
Y Resolution                    : 600
Software                        : Adobe Photoshop CS2 Windows
Modify Date                     : 2009:05:19 10:56:21
Artist                          : IPTC CONTACT PANEL: CREATOR
Copyright                       : IPTC STATUS PANEL: COPYRIGHT NOTICE
Exif Image Width                : 300
Exif Image Height               : 379
Current IPTC Digest             : dac12b6161bf1efad456c84efd43e62e
Application Record Version      : 2
Caption-Abstract                : IPTC CONTENT PANEL: DESCRIPTION
Creator Tool                    : Adobe Photoshop CS2 Windows
Create Date                     : 2009:05:19 09:46:29-07:00
Metadata Date                   : 2009:05:19 10:56:21-07:00
Title                           : IPTC STATUS PANEL: TITLE
Creator                         : IPTC CONTACT PANEL: CREATOR
Description                     : IPTC CONTENT PANEL: DESCRIPTION
Rights                          : IPTC STATUS PANEL: COPYRIGHT NOTICE
Date Created                    : 2007:11:19
City                            : IPTC IMAGE PANEL: CITY
State                           : IPTC IMAGE PANEL: STATE/PROVINCE
Country                         : IPTC IMAGE PANEL: COUNTRY
ICC Profile Name                : Adobe RGB (1998)
Image Width                     : 300
Image Height                    : 379
```

This made it possible to compare the sanitized file with its original copy.

## Key Concepts

- **Metadata sanitization:** The removal of information embedded in a file.
- **`-all=`:** Instructs ExifTool to remove the metadata it can remove from the file.
- **Original file:** ExifTool preserves a copy using the `_original` suffix.
- **Metadata removal:** Removing metadata can affect components associated with the file, as indicated by the warning about the ICC profile.

## Activity Workflow

```text
Original image
      ↓
exiftool -all=
      ↓
Metadata removed
      ↓
_original file preserved
      ↓
Comparison using ExifTool
```

## Result

The main metadata was successfully removed from `IPTCpanel.jpg`, and the `IPTCpanel.jpg_original` copy was verified to retain the original information.

## Evidence

**View Evidence — Module 12 / Classes 47–48**

**Required screenshot:** Step 5 — the output of `exiftool IPTCpanel.jpg` after metadata removal.

---

[Back to Classes 47–48](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
