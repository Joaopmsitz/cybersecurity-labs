# Atividade 12.8 — Escrevendo metadados no Kali Linux

Nesta atividade foi utilizado o **ExifTool** para adicionar e modificar metadados de uma imagem JPEG, incluindo informações de direitos autorais, autor e datas.

> **Observação:** credenciais utilizadas no ambiente de laboratório não são registradas neste documento.

## Objetivo

* Escrever metadados em arquivos digitais.
* Alterar informações de direitos autorais e autoria.
* Modificar datas armazenadas nos metadados.
* Observar o resultado das alterações utilizando o ExifTool.

## Procedimento

### 1. Acesso ao Kali Linux

O Kali Linux foi acessado via RDP pelo endereço `192.168.98.40`.

Foi obtido acesso administrativo:

```bash
sudo -i
```

### 2. Verificação dos arquivos

Foi acessado o diretório das atividades:

```bash
cd /home/aluno/Documentos/Arquivos
```

Os arquivos disponíveis eram:

```bash
ls
```

```text
contrato_08_2021.pdf  IPTCpanel.jpg IPTCpanel.jpg_original
```

### 3. Adição de informações de direitos autorais

Como a imagem `IPTCpanel.jpg` havia sido sanitizada na atividade anterior, foram adicionados novos metadados:

```bash
exiftool -rights="Direitos autorais do Professor" -CopyrightNotice="Direitos autorais do Professor" IPTCpanel.jpg
```

Saída:

```text
    1 image files updated
```

Foram utilizados dois campos diferentes para representar a informação de direitos autorais:

* `-rights`
* `-CopyrightNotice`

### 4. Verificação dos metadados

```bash
exiftool IPTCpanel.jpg
```

Trecho relevante:

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

Os dois campos foram registrados no arquivo.

### 5. Adição do autor

Foi adicionado o nome do autor utilizando XMP:

```bash
exiftool -XMP-dc:Creator="Prof. Max" "IPTCpanel.jpg"
```

Saída:

```text
    1 image files updated
```

A alteração foi verificada:

```bash
exiftool IPTCpanel.jpg
```

Trecho relevante:

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

### 6. Alteração das datas

Foi utilizada a opção `-AllDates` para definir as datas armazenadas nos metadados:

```bash
exiftool -AllDates="1917:12:12 06:00:00" "IPTCpanel.jpg"
```

Saída:

```text
    1 image files updated
```

Em seguida, os metadados foram consultados novamente:

```bash
exiftool IPTCpanel.jpg
```

Trecho principal:

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

O comando alterou os campos de data suportados pelo `-AllDates`, enquanto as datas do sistema de arquivos continuaram correspondendo ao momento da modificação do arquivo.

### 7. Limpeza dos arquivos

Ao final da atividade, os arquivos foram removidos:

```bash
rm -r *.*
```

Em seguida:

```bash
ls
```

O diretório ficou sem os arquivos utilizados na atividade.

## Conceitos

* **Metadados:** informações armazenadas dentro ou associadas ao arquivo.
* **XMP/IPTC/EXIF:** diferentes estruturas utilizadas para armazenar informações sobre arquivos de mídia.
* **`-rights` / `-CopyrightNotice`:** campos relacionados a direitos autorais.
* **`-XMP-dc:Creator`:** campo utilizado para registrar o criador.
* **`-AllDates`:** altera os principais campos de data suportados pelo ExifTool.

## Fluxo

```text
Imagem sem metadados
        ↓
Adicionar direitos autorais
        ↓
Adicionar autor
        ↓
Alterar datas
        ↓
Consultar com ExifTool
        ↓
Remover arquivos utilizados
```

## Resultado

Foi possível escrever e alterar metadados da imagem utilizando o ExifTool, incluindo direitos autorais, autoria e datas.

## Evidência

[**Evidências — Módulo 12 / Aulas 43 e 44**](../evidencias.pdf)

**Print solicitado:** passo 7 — saída do `exiftool IPTCpanel.jpg` após a alteração das datas.
