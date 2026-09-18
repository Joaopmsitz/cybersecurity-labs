# Atividade 6.7 — Encurtando Links e Gerando QR Code no Kali Linux

## Objetivo

Nesta atividade foi utilizado o Kali Linux para realizar duas tarefas relacionadas ao gerenciamento e compartilhamento de URLs:

1. encurtar uma URL utilizando o serviço TinyURL;
2. gerar um **QR Code** a partir da URL encurtada utilizando a ferramenta `qrencode`.

O exercício demonstra como ferramentas de linha de comando podem ser utilizadas para realizar solicitações HTTP e gerar arquivos de imagem a partir de dados textuais.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório de trabalho:** `/home/aluno/Documentos`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="j7m3q8"
sudo -i
```

---

## 2. Encurtando uma URL com TinyURL

Foi utilizado o `curl` para realizar uma solicitação HTTP à API do TinyURL.

A URL de destino utilizada no laboratório foi:

```text id="v5r2n9"
https://esr.rnp.br/cursos/?_formacao_cursos=seguranca
```

O comando executado foi:

```bash id="q8w4m6"
curl -s -i https://tinyurl.com/api-create.php?url=https://esr.rnp.br/cursos/?_formacao_cursos=seguranca
```

A opção `-s` reduz a saída adicional do `curl`, enquanto `-i` inclui os cabeçalhos HTTP da resposta.

Saída observada:

```text id="p3x7k2"
HTTP/2 200 
date: Sun, 11 Feb 2024 01:16:28 GMT
content-type: text/plain; charset=UTF-8
cache-control: max-age=86400, public
x-content-type-options: nosniff
x-xss-protection: 1; mode=block
last-modified: Sun, 11 Feb 2024 01:16:28 GMT
cf-cache-status: MISS
set-cookie: __cf_bm=5NBi9lCZxPG_WViAebyvYj7f.7bCxcjdVoWgL.aJ7KXFbXMBsERBISM7g7aZxZJ+weYUXMmS2X97U9GuyijoxiU=; path=/; expires=Sun, 11-Feb-24 01:46:28 GMT; domain=.tinyurl.com; HttpOnly; Secure; SameSite=None
strict-transport-security: max-age=31536000; includeSubDomains; preload
server: cloudflare
cf-ray: 8538bf24ba5b0a05-IAD
alt-svc: h3=":443"; ma=86400

http://tinyurl.com/27ldrg4o
```

A resposta `HTTP/2 200` indica que a solicitação foi processada com sucesso.

O corpo da resposta apresentou a URL encurtada:

```text id="s4v9m1"
http://tinyurl.com/27ldrg4o
```

---

## 3. Entendendo a solicitação

O comando utilizado pode ser representado da seguinte forma:

```text id="a6k3p9"
curl
 │
 ├── -s → saída silenciosa
 ├── -i → inclui cabeçalhos HTTP
 │
 └── TinyURL API
       │
       └── URL de destino
             ↓
       URL encurtada
```

O código de status:

```text id="f2m7q5"
HTTP/2 200
```

representa uma resposta HTTP bem-sucedida.

A URL retornada pelo serviço foi:

```text id="n8c4w1"
http://tinyurl.com/27ldrg4o
```

---

## 4. Testando o link encurtado

A URL encurtada foi aberta no Mozilla Firefox:

```text id="r7x3m5"
https://tinyurl.com/27ldrg4o
```

O objetivo foi verificar o funcionamento do endereço gerado pelo serviço de encurtamento.

Após a validação, o navegador foi fechado.

---

## 5. Gerando o QR Code

Primeiramente, foi acessado o diretório de trabalho:

```bash id="k2v9p6"
cd /home/aluno/Documentos
```

O conteúdo do diretório foi verificado:

```bash id="u4m8q1"
ls
```

Em seguida, foi utilizado o `qrencode` para gerar uma imagem contendo a URL encurtada:

```bash id="c6x2r9"
qrencode -o qr_code.png "https://tinyurl.com/27ldrg4o"
```

Depois da geração, foi executado novamente:

```bash id="w5n3j7"
ls
```

Resultado:

```text id="e8q1v4"
qr_code.png
```

O arquivo `qr_code.png` contém o QR Code correspondente à URL utilizada.

**Este é o passo solicitado para a evidência da atividade.**

---

## Como o comando `qrencode` funciona

O comando utilizado foi:

```bash id="b7m4x9"
qrencode -o qr_code.png "https://tinyurl.com/27ldrg4o"
```

Seus componentes são:

### `qrencode`

É o programa responsável por gerar o QR Code.

### `-o`

Define o arquivo de saída.

Neste caso:

```text id="z1c8p3"
-o qr_code.png
```

indica que a imagem será salva como `qr_code.png`.

### URL

O último argumento representa o conteúdo que será codificado:

```text id="j5r9k2"
https://tinyurl.com/27ldrg4o
```

Ao ler o QR Code, um dispositivo compatível poderá interpretar esse conteúdo como uma URL.

---

## Visualizando o QR Code

O arquivo:

```text id="m4x7q1"
/home/aluno/Documentos/qr_code.png
```

foi aberto através do Thunar utilizando o visualizador de imagens.

A visualização permitiu confirmar a criação da imagem contendo o QR Code.

O código poderia ser lido por um dispositivo compatível, como um smartphone, para acessar a URL armazenada.

---

## Conceitos envolvidos

### URL encurtada

Um serviço de encurtamento associa uma URL longa a um endereço mais curto.

No laboratório, a URL de destino:

```text id="s3n8v5"
https://esr.rnp.br/cursos/?_formacao_cursos=seguranca
```

foi transformada em:

```text id="y6p2k9"
http://tinyurl.com/27ldrg4o
```

Isso facilita a utilização da URL em situações nas quais um endereço menor é mais conveniente.

### QR Code

Um **QR Code** é um código bidimensional capaz de armazenar informações que podem ser interpretadas por dispositivos compatíveis.

Neste exercício, o conteúdo armazenado foi uma URL.

### `curl`

O `curl` foi utilizado para enviar a solicitação à API do serviço de encurtamento:

```bash id="h4w7m2"
curl -s -i ...
```

Isso demonstra que serviços web podem ser acessados diretamente pela linha de comando.

### `qrencode`

O `qrencode` converte o conteúdo fornecido em uma imagem QR.

Neste caso:

```text id="n2q8c5"
URL → qrencode → qr_code.png
```

---

## Resultado

A atividade permitiu:

1. realizar uma solicitação HTTP à API do TinyURL;
2. receber uma URL encurtada;
3. verificar o código de resposta HTTP `200`;
4. testar a URL encurtada no navegador;
5. utilizar o `qrencode` para transformar a URL em um QR Code;
6. gerar o arquivo `qr_code.png`;
7. visualizar o QR Code no Kali Linux.

A URL encurtada obtida no laboratório foi:

```text id="p8m4x6"
http://tinyurl.com/27ldrg4o
```

E o arquivo gerado foi:

```text id="v3k7q1"
qr_code.png
```

---

## Limpeza

Após a visualização do QR Code, o arquivo foi removido:

```bash id="q6n2m8"
rm qr_code.png
```

O visualizador de imagens, Thunar e o terminal foram então fechados.

---

## Evidência

A evidência desta atividade corresponde ao **passo 5**, mostrando o QR Code gerado no diretório `Documentos`.

[**Evidências — Módulo 6 / Aulas 3 e 4**](../evidencias.pdf)
