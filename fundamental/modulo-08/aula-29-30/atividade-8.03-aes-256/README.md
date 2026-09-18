# Atividade 8.3 — Cifrando e decifrando um arquivo com AES-256 no Kali Linux

## Objetivo

Utilizar o **OpenSSL** para cifrar e decifrar um arquivo utilizando **AES-256 no modo CTR**, demonstrando o processo de proteção de um arquivo e sua posterior recuperação mediante a chave utilizada na cifragem.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo:** AES-256-CTR
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `My_shoe.jpg`
* **Arquivo cifrado:** `arquivo_criptografado`
* **Arquivo recuperado:** `My_shoe2.jpg`

> A senha utilizada durante o laboratório não é registrada neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash
sudo -i
```

---

## 2. Acesso ao diretório de trabalho

Foi acessado o diretório utilizado para armazenar os arquivos da atividade:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Download do arquivo utilizado no laboratório

Foi baixada uma imagem JPG da Wikimedia Commons para ser utilizada como arquivo de entrada:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
```

Saída registrada:

```text
--2024-03-03 20:42:50--  https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 1297035 (1,2M) [image/jpeg]
Salvando em: “My_shoe.jpg”

My_shoe.jpg                    100%[===================================================>]   1,24M  7,35MB/s    em 0,2s    

2024-03-03 20:42:51 (7,35 MB/s) - “My_shoe.jpg” salvo [1297035/1297035]
```

A imagem foi aberta no **Thunar** para confirmar visualmente o arquivo antes da cifragem.

---

## 4. Cifragem utilizando AES-256-CTR

Primeiramente, foi verificado o conteúdo do diretório:

```bash
ls
```

Saída:

```text
arquivo_criptografado  My_shoe.jpg
```

Em seguida, foi utilizado o OpenSSL para cifrar a imagem:

```bash
openssl enc -aes-256-ctr -salt -in My_shoe.jpg -out arquivo_criptografado
```

Durante o processo, foi solicitada uma senha para a cifragem:

```text
enter AES-256-CTR encryption password:
Verifying - enter AES-256-CTR encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Após a execução, o arquivo cifrado foi criado.

### Parâmetros utilizados

* `enc` — utiliza o módulo de cifragem de arquivos do OpenSSL;
* `-aes-256-ctr` — utiliza AES com chave de 256 bits no modo CTR;
* `-salt` — adiciona um salt ao processo de derivação da chave;
* `-in My_shoe.jpg` — define o arquivo original como entrada;
* `-out arquivo_criptografado` — define o arquivo de saída cifrado.

O OpenSSL também apresentou um aviso sobre a **derivação de chave legada**, recomendando o uso de `-iter` ou `-pbkdf2` em operações modernas.

---

## 5. Remoção do original e decifragem

Para verificar se o arquivo poderia ser recuperado a partir da versão cifrada, o arquivo original foi removido:

```bash
rm My_shoe.jpg
```

Em seguida, foi confirmado que restava apenas o arquivo cifrado:

```bash
ls
```

Saída:

```text
arquivo_criptografado
```

O arquivo foi então decifrado utilizando o OpenSSL:

```bash
openssl enc -d -aes-256-ctr -in arquivo_criptografado -out My_shoe2.jpg
```

Foi solicitada a senha utilizada anteriormente:

```text
enter AES-256-CTR decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Por fim, foi utilizado `ls` para verificar o arquivo recuperado:

```bash
ls
```

Saída:

```text
arquivo_criptografado  My_shoe2.jpg
```

A presença de `My_shoe2.jpg` demonstra que o conteúdo foi recuperado a partir do arquivo cifrado.

A imagem recuperada também foi aberta no **Thunar** para verificar visualmente o resultado da decifragem.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 6**, demonstrando a remoção do arquivo original, a existência do arquivo cifrado, a execução da decifragem e a criação da imagem recuperada:

```text
rm My_shoe.jpg
ls
arquivo_criptografado

openssl enc -d -aes-256-ctr -in arquivo_criptografado -out My_shoe2.jpg
enter AES-256-CTR decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls
arquivo_criptografado  My_shoe2.jpg
```

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)
