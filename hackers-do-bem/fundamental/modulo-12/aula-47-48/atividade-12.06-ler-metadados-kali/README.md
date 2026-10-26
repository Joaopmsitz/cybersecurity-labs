# Activity 12.06 — Reading Metadata on Kali Linux

Metadata from files was examined in this activity using ExifTool on Kali Linux. A JPEG image and a PDF document were analyzed, revealing information such as dates, software used, author, copyright, file characteristics, and format-specific information.

> **Note:** Credentials used in the lab environment are not recorded in this document.

## Objective

- Identify metadata present in digital files.
- Use ExifTool to analyze files.
- Examine information from JPEG and PDF files.
- Understand how metadata can provide relevant information during forensic analysis.

## Procedure

### 1. Accessing Kali Linux

Kali Linux was accessed via RDP using the address `192.168.98.40`.

Administrative privileges were obtained using:

```bash
sudo -i
```

### 2. Downloading the Image

The directory used for the activity files was accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

Initially, the directory was empty. The image was then downloaded using `wget`:

```bash
wget http://metadatadeluxe.pbworks.com/f/1242756531/IPTCpanel.jpg
```

Output:

```text
--2025-12-06 19:45:10--  http://metadatadeluxe.pbworks.com/f/1242756531/IPTCpanel.jpg
Resolvendo metadatadeluxe.pbworks.com (metadatadeluxe.pbworks.com)... 208.96.18.238, 208.96.18.237
Conectando-se a metadatadeluxe.pbworks.com (metadatadeluxe.pbworks.com)|208.96.18.238|:80... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 86782 (85K) [image/jpeg]
Salvando em: “IPTCpanel.jpg”

IPTCpanel.jpg              100%[=======================================>]  84,75K  --.-KB/s    em 0,1s    

2025-12-06 19:45:10 (603 KB/s) - “IPTCpanel.jpg” salvo [86782/86782]
```

The presence of the file was confirmed:

```bash
ls
```

Output:

```text
IPTCpanel.jpg
```

### 3. Analyzing the Image Metadata

ExifTool was used to analyze the image:

```bash
exiftool IPTCpanel.jpg
```

The information found included:

```text
ExifTool Version Number         : 13.36
File Name                       : IPTCpanel.jpg
Directory                       : .
File Size                       : 87 kB
File Modification Date/Time     : 2023:01:26 13:08:28-03:00
File Access Date/Time           : 2025:12:06 19:45:10-03:00
File Inode Change Date/Time     : 2025:12:06 19:45:10-03:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Exif Byte Order                 : Big-endian (Motorola, MM)
Image Description               : IPTC CONTENT PANEL: DESCRIPTION
Orientation                     : Horizontal (normal)
X Resolution                    : 600
Y Resolution                    : 600
Resolution Unit                 : inches
Software                        : Adobe Photoshop CS2 Windows
Modify Date                     : 2009:05:19 10:56:21
Artist                          : IPTC CONTACT PANEL: CREATOR
Copyright                       : IPTC STATUS PANEL: COPYRIGHT NOTICE
Color Space                     : Uncalibrated
Exif Image Width               : 300
Exif Image Height              : 379
```

The output also included several IPTC, XMP, and Photoshop fields, including information about the author, copyright, title, description, location, dates, and document identifiers.

Among the relevant fields were:

```text
Creator Tool                    : Adobe Photoshop CS2 Windows
Create Date                     : 2009:05:19 09:46:29-07:00
Metadata Date                   : 2009:05:19 10:56:21-07:00
Title                           : IPTC STATUS PANEL: TITLE
Creator                         : IPTC CONTACT PANEL: CREATOR
Description                     : IPTC CONTENT PANEL: DESCRIPTION
Subject                         : IPTC CONTENT PANEL:, KEYWORDS
Rights                          : IPTC STATUS PANEL: COPYRIGHT NOTICE
Date Created                    : 2007:11:19
City                            : IPTC IMAGE PANEL: CITY
State                           : IPTC IMAGE PANEL: STATE/PROVINCE
Country                         : IPTC IMAGE PANEL: COUNTRY
```

Technical image information was also identified, including:

```text
Image Width                     : 300
Image Height                    : 379
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)
Image Size                      : 300x379
Megapixels                      : 0.114
```

### 4. Main Information Identified

The analysis revealed, among other details:

- **File Name:** `IPTCpanel.jpg`
- **File Size:** 87 kB
- **File Type:** JPEG
- **MIME Type:** `image/jpeg`
- **JFIF Version:** 1.02
- **Orientation:** Horizontal
- **Resolution:** 600 × 600
- **Software:** Adobe Photoshop CS2 Windows
- **Image dimensions:** 300 × 379 pixels
- **Create Date:** May 19, 2009
- **Date Created:** November 19, 2007
- **Copyright:** IPTC copyright notice field
- **Creator:** IPTC creator field

These details demonstrate that an image can contain information beyond its visual content.

### 5. Downloading the PDF

Still in the files directory, a contract from Brazil's National Council of Justice (Conselho Nacional de Justiça — CNJ) was downloaded:

```bash
wget https://www.cnj.jus.br/wp-content/uploads/2021/07/contrato_08_2021.pdf
```

Output:

```text
--2025-12-06 19:49:57--  https://www.cnj.jus.br/wp-content/uploads/2021/07/contrato_08_2021.pdf
Resolvendo www.cnj.jus.br (www.cnj.jus.br)... 3.167.69.77, 3.167.69.122, 3.167.69.51, ...
Conectando-se a www.cnj.jus.br (www.cnj.jus.br)|3.167.69.77|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 22074478 (21M) [application/pdf]
Salvando em: “contrato_08_2021.pdf”

contrato_08_2021.pdf       100%[=======================================>]  21,05M  16,8MB/s    em 1,3s    

2025-12-06 19:49:59 (16,8 MB/s) - “contrato_08_2021.pdf” salvo [22074478/22074478]
```

The presence of both files was confirmed:

```bash
ls
```

Output:

```text
contrato_08_2021.pdf  IPTCpanel.jpg
```

### 6. Analyzing the PDF Metadata

ExifTool was used again:

```bash
exiftool contrato_08_2021.pdf
```

Output:

```text
ExifTool Version Number     : 13.36
File Name                   : contrato_08_2021.pdf
Directory                   : .
File Size                   : 22 MB
File Modification Date/Time : 2022:03:07 15:23:03-03:00
File Access Date/Time       : 2025:12:06 19:49:59-03:00
File Inode Change Date/Time : 2025:12:06 19:49:59-03:00
File Permissions            : -rw-r--r--
File Type                   : PDF
File Type Extension         : pdf
MIME Type                   : application/pdf
Linearized                  : No
Page Count                  : 626
Warning                     : Duplicate 'DR' entry in dictionary (ignored)
Has XFA                     : No
Language                    : pt-BR
Tagged PDF                  : Yes
XMP Toolkit                 : 3-Heights(TM) XMP Library 4.8.25.2
Creator Tool                : Microsoft® Word para Microsoft 365
Create Date                 : 2021:07:06 17:28:51-03:00
Modify Date                 : 2021:07:06 21:02:09Z
Metadata Date               : 2021:07:06 21:02:09Z
Document ID                 : uuid:9EF429E5-0920-4C12-B890-66E34903C95E
Instance ID                 : urn:uuid:C816A848-8634-4059-B293-E647B1DFC85F
Producer                    : 3-Heights(TM) PDF Security Shell 4.8.25.2
PDF Version                 : 1.7
Format                      : application/pdf
```

The identified information included the page count, language, software used to create the document, creation and modification dates, PDF version, and document identifiers.

## Key Concepts

- **Metadata:** Information associated with a file that describes its characteristics, origin, or history.
- **ExifTool:** A tool used to read and manipulate metadata from various file formats.
- **EXIF/IPTC/XMP:** Standards and structures used to store different types of metadata.
- **Forensic analysis:** Metadata can provide supporting evidence for understanding the origin and history of digital files.

## Activity Workflow

```text
Digital file
      ↓
Download on Kali Linux
      ↓
ExifTool
      ↓
Read metadata
      ↓
Identify dates, software,
author, format, and other information
```

## Result

ExifTool was used to identify metadata from a JPEG image and a PDF document, demonstrating how digital files can contain information useful for technical and forensic analysis.

## Evidence

**View Evidence — Module 12 / Classes 47–48**

**Required screenshot:** Step 8 — the output of `exiftool contrato_08_2021.pdf`.

---

[Back to Classes 47–48](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
