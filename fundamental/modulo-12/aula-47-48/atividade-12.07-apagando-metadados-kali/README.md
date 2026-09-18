# Atividade 12.7 — Apagando metadados no Kali Linux

Nesta atividade foi utilizado o **ExifTool** para remover metadados de uma imagem JPEG e comparar o arquivo modificado com o arquivo original preservado automaticamente pela ferramenta.

> **Observação:** credenciais utilizadas no ambiente de laboratório não são registradas neste documento.

## Objetivo

* Remover metadados de uma imagem.
* Identificar a diferença entre o arquivo original e o arquivo tratado.
* Utilizar o ExifTool para sanitização de metadados.
* Observar quais informações permanecem após a remoção.

## Procedimento

### 1. Acesso ao Kali Linux

O Kali Linux foi acessado via RDP pelo endereço `192.168.98.40`.

Foi aberto um terminal e obtido acesso administrativo:

```bash
sudo -i
```

### 2. Verificação dos arquivos

Foi acessado o diretório utilizado na atividade anterior:

```bash
cd /home/aluno/Documentos/Arquivos
```

Os arquivos existentes eram:

```bash
ls
```

```text
contrato_08_2021.pdf  IPTCpanel.jpg
```

### 3. Remoção dos metadados

Foi utilizado o parâmetro `-all=` do ExifTool para remover os metadados da imagem:

```bash
exiftool -all= IPTCpanel.jpg
```

Saída:

```text
Warning: ICC_Profile deleted. Image colors may be affected - IPTCpanel.jpg
    1 image files updated
```

O ExifTool atualizou a imagem e preservou automaticamente o arquivo original como `IPTCpanel.jpg_original`.

### 4. Verificação dos arquivos

```bash
ls
```

```text
contrato_08_2021.pdf  IPTCpanel.jpg  IPTCpanel.jpg_original
```

### 5. Verificação da imagem após a remoção

Foi executado:

```bash
exiftool IPTCpanel.jpg
```

Saída:

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

Comparando com a análise anterior, diversos campos de EXIF, IPTC, XMP e Photoshop deixaram de aparecer.

### 6. Verificação do arquivo original

O arquivo preservado pelo ExifTool foi analisado:

```bash
exiftool IPTCpanel.jpg_original
```

A saída manteve os metadados presentes originalmente, incluindo informações como:

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

Isso permitiu comparar o arquivo sanitizado com sua cópia original.

## Conceitos

* **Sanitização de metadados:** remoção de informações incorporadas ao arquivo.
* **`-all=`:** instrui o ExifTool a remover os metadados que puder remover do arquivo.
* **Arquivo original:** o ExifTool preserva uma cópia com o sufixo `_original`.
* A remoção de metadados pode afetar componentes associados ao arquivo, como indicado pelo aviso sobre o perfil ICC.

## Fluxo

```text
Imagem original
      ↓
exiftool -all=
      ↓
Metadados removidos
      ↓
Arquivo _original preservado
      ↓
Comparação com ExifTool
```

## Resultado

Foi possível remover os principais metadados da imagem `IPTCpanel.jpg` e verificar que a cópia `IPTCpanel.jpg_original` preservou as informações originais.

## Evidência

[**Evidências — Módulo 12 / Aulas 43 e 44**](../evidencias.pdf)

**Print solicitado:** passo 5 — saída do `exiftool IPTCpanel.jpg` após a remoção dos metadados.
