# Atividade 12.6 — Ler metadados no Kali Linux

Nesta atividade foi realizada a leitura de metadados de arquivos utilizando o **ExifTool** no Kali Linux. Foram analisados uma imagem JPEG e um documento PDF, observando informações como datas, software utilizado, autor, direitos autorais, características do arquivo e informações específicas dos formatos.

> **Observação:** credenciais utilizadas no ambiente de laboratório não são registradas neste documento.

## Objetivo

* Identificar metadados presentes em arquivos digitais.
* Utilizar o ExifTool para análise de arquivos.
* Observar informações de arquivos JPEG e PDF.
* Compreender como metadados podem fornecer informações relevantes em uma análise forense.

## Procedimento

### 1. Acesso ao Kali Linux

O Kali Linux foi acessado via RDP pelo endereço `192.168.98.40`.

Para obter privilégios administrativos:

```bash
sudo -i
```

### 2. Download da imagem

Foi acessado o diretório utilizado para os arquivos da atividade:

```bash
cd /home/aluno/Documentos/Arquivos
```

Inicialmente, o diretório estava vazio. Em seguida, a imagem foi baixada utilizando `wget`:

```bash
wget http://metadatadeluxe.pbworks.com/f/1242756531/IPTCpanel.jpg
```

Saída:

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

A presença do arquivo foi confirmada:

```bash
ls
```

```text
IPTCpanel.jpg
```

### 3. Análise dos metadados da imagem

O ExifTool foi utilizado para analisar a imagem:

```bash
exiftool IPTCpanel.jpg
```

Entre as informações encontradas estavam:

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

A saída também apresentou diversos campos IPTC, XMP e Photoshop, incluindo informações de autor, direitos autorais, título, descrição, localização, datas e identificadores do documento.

Entre os campos relevantes estavam:

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

Também foram identificadas informações técnicas da imagem, como:

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

### 4. Principais informações identificadas

A análise permitiu observar, entre outros dados:

* **File Name:** `IPTCpanel.jpg`
* **File Size:** `87 kB`
* **File Type:** JPEG
* **MIME Type:** `image/jpeg`
* **JFIF Version:** `1.02`
* **Orientation:** horizontal
* **Resolution:** 600 × 600
* **Software:** Adobe Photoshop CS2 Windows
* **Image dimensions:** 300 × 379 pixels
* **Create Date:** 19/05/2009
* **Date Created:** 19/11/2007
* **Copyright:** campo IPTC de direitos autorais
* **Creator:** campo IPTC de criador

Esses dados demonstram que uma imagem pode carregar informações além do seu conteúdo visual.

### 5. Download do PDF

Ainda no diretório de arquivos, foi baixado um contrato do Conselho Nacional de Justiça:

```bash
wget https://www.cnj.jus.br/wp-content/uploads/2021/07/contrato_08_2021.pdf
```

Saída:

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

A existência dos arquivos foi confirmada:

```bash
ls
```

```text
contrato_08_2021.pdf  IPTCpanel.jpg
```

### 6. Análise dos metadados do PDF

O ExifTool foi utilizado novamente:

```bash
exiftool contrato_08_2021.pdf
```

Saída:

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

Entre os dados identificados estão o número de páginas, idioma, ferramenta utilizada na criação, datas de criação/modificação, versão do PDF e identificadores do documento.

## Conceitos

* **Metadados:** informações associadas a um arquivo que descrevem características, origem ou histórico.
* **ExifTool:** ferramenta utilizada para ler e manipular metadados de diversos formatos.
* **EXIF/IPTC/XMP:** padrões e estruturas utilizadas para armazenar diferentes tipos de metadados.
* **Análise forense:** metadados podem fornecer elementos auxiliares para compreender a origem e o histórico de arquivos digitais.

## Fluxo

```text
Arquivo digital
      ↓
Download no Kali Linux
      ↓
ExifTool
      ↓
Leitura dos metadados
      ↓
Identificação de datas, software,
autor, formato e outras informações
```

## Resultado

Foi possível utilizar o ExifTool para identificar metadados de uma imagem JPEG e de um documento PDF, demonstrando como arquivos digitais podem conter informações úteis para análise técnica e forense.

## Evidência

[**Evidências — Módulo 12 / Aulas 43 e 44**](../evidencias.pdf)

**Print solicitado:** passo 8 — saída do `exiftool contrato_08_2021.pdf`.
