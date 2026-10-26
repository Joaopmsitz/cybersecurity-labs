# Activity 12.08 — Writing Metadata on Kali Linux

In this activity, ExifTool was used to add and modify metadata in a JPEG image, including copyright information, authorship, and dates.

> **Note:** Credentials used in the lab environment are not recorded in this document.

## Objective

- Write metadata to digital files.
- Modify copyright and authorship information.
- Change dates stored in metadata.
- Examine the results of these changes using ExifTool.

## Procedure

### 1. Accessing Kali Linux

Kali Linux was accessed via RDP using the address `192.168.98.40`.

Administrative privileges were obtained using:

```bash
sudo -i
```

### 2. Checking the Files

The directory used for the activities was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

The available files were listed using:

```bash
ls
```

Output:

```text
contrato_08_2021.pdf  IPTCpanel.jpg IPTCpanel.jpg_original
```

### 3. Adding Copyright Information

Because `IPTCpanel.jpg` had been sanitized during the previous activity, new metadata was added:

```bash
exiftool -rights="Direitos autorais do Professor" -CopyrightNotice="Direitos autorais do Professor" IPTCpanel.jpg
```

Output:

```text
    1 image files updated
```

Two different fields were used to represent the copyright information:

- `-rights`
- `-CopyrightNotice`

### 4. Verifying the Metadata

The metadata was inspected using:

```bash
exiftool IPTCpanel.jpg
```

Relevant output:

```text
ExifTool Version Number         : 13.36
File Name                       : IPTCpanel.jpg
File Size                       : 54 kB
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Current IPTC Digest             : 86e482c077aedfe38855ec2781d06810
Copyright Notice                : Direitos autorais do Professor
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 13.36
Rights                          : Direitos autorais do Professor
Image Width                     : 300
Image Height                    : 379
```

Both fields were recorded in the file.

### 5. Adding the Author

The author's name was added using XMP:

```bash
exiftool -XMP-dc:Creator="Prof. Max" "IPTCpanel.jpg"
```

Output:

```text
    1 image files updated
```

The change was verified using:

```bash
exiftool IPTCpanel.jpg
```

Relevant output:

```text
ExifTool Version Number         : 13.36
File Name                       : IPTCpanel.jpg
File Size                       : 54 kB
File Type                       : JPEG
MIME Type                       : image/jpeg
Copyright Notice                : Direitos autorais do Professor
Application Record Version      : 4
Creator                         : Prof. Max
Rights                          : Direitos autorais do Professor
Image Width                     : 300
Image Height                    : 379
```

### 6. Modifying the Dates

The `-AllDates` option was used to set the dates stored in the metadata:

```bash
exiftool -AllDates="1917:12:12 06:00:00" "IPTCpanel.jpg"
```

Output:

```text
    1 image files updated
```

The metadata was then queried again:

```bash
exiftool IPTCpanel.jpg
```

Main output:

```text
ExifTool Version Number         : 13.36
File Name                       : IPTCpanel.jpg
File Size                       : 55 kB
File Type                       : JPEG
MIME Type                       : image/jpeg
Exif Byte Order                 : Big-endian (Motorola, MM)
Modify Date                     : 1917:12:12 06:00:00
Y Cb Cr Positioning             : Centered
Exif Version                    : 0232
Date/Time Original              : 1917:12:12 06:00:00
Create Date                     : 1917:12:12 06:00:00
Components Configuration        : Y, Cb, Cr, -
Color Space                     : Uncalibrated
Current IPTC Digest             : 86e482c077aedfe38855ec2781d06810
Copyright Notice                : Direitos autorais do Professor
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 13.36
Creator                         : Prof. Max
Rights                          : Direitos autorais do Professor
Image Width                     : 300
Image Height                    : 379
Image Size                      : 300x379
Megapixels                     : 0.114
```

The command modified the date fields supported by `-AllDates`, while the filesystem dates continued to reflect the time when the file was modified.

### 7. Cleaning Up the Files

At the end of the activity, the files were removed using:

```bash
rm -r *.*
```

The following command was then executed:

```bash
ls
```

The directory was left without the files used in the activity.

## Key Concepts

- **Metadata:** Information stored within or associated with a file.
- **XMP/IPTC/EXIF:** Different structures used to store information about media files.
- **`-rights` / `-CopyrightNotice`:** Fields associated with copyright information.
- **`-XMP-dc:Creator`:** A field used to record the creator.
- **`-AllDates`:** Modifies the main date fields supported by ExifTool.

## Activity Workflow

```text
Image without metadata
        ↓
Add copyright information
        ↓
Add author
        ↓
Modify dates
        ↓
Inspect with ExifTool
        ↓
Remove the files used
```

## Result

ExifTool was used to write and modify metadata in the image, including copyright information, authorship, and dates.

## Evidence

**View Evidence — Module 12 / Classes 47–48**

**Required screenshot:** Step 7 — the output of `exiftool IPTCpanel.jpg` after modifying the dates.

---

[Back to Classes 47–48](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
