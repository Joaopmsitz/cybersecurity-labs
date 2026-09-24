# Atividade 8.1 — Usando a Esteganografia no Kali Linux

## Objetivo

Utilizar **esteganografia** para ocultar o conteúdo de um arquivo de texto dentro de uma imagem JPG e, posteriormente, recuperar o arquivo oculto a partir da imagem.

Para isso, foi utilizado o `steghide`, ferramenta capaz de incorporar dados em arquivos de cobertura, como imagens e arquivos de áudio.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Steghide
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo de texto:** `mensagem.txt`
* **Arquivo de cobertura:** `Marcel_Proust_1895-cropped.jpg`

> As credenciais e senhas utilizadas no ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi aberto o Terminal e obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Criação do diretório de trabalho

Foi criado o diretório `Arquivos` dentro de `Documentos`:

```bash
mkdir -m 777 /home/aluno/Documentos/Arquivos
```

Em seguida, o diretório foi acessado:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Criação da mensagem

Foi criado o arquivo `mensagem.txt`:

```bash
nano mensagem.txt
```

O conteúdo inserido foi:

```text
Hackers do bem com Esteganografia!
```

Esse arquivo será utilizado como conteúdo oculto dentro da imagem.

---

## 4. Download da imagem

Foi utilizada uma imagem JPG obtida da Wikimedia:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/1/1b/Marcel_Proust_1895-cropped.jpg
```

Saída registrada no laboratório:

```text
--2024-03-03 20:07:52--  https://upload.wikimedia.org/wikipedia/commons/1/1b/Marcel_Proust_1895-cropped.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 657966 (643K) [image/jpeg]
Salvando em: “Marcel_Proust_1895-cropped.jpg”

Marcel_Proust_1895-cropped.jpg 100%[===================================================>] 642,54K  --.-KB/s    em 0,1s    

2024-03-03 20:07:52 (4,62 MB/s) - “Marcel_Proust_1895-cropped.jpg” salvo [657966/657966]
```

---

## 5. Verificação dos arquivos

Foi utilizado `ls` para confirmar que tanto a imagem quanto o arquivo de texto estavam presentes:

```bash
ls
```

Saída:

```text
Marcel_Proust_1895-cropped.jpg  mensagem.txt
```

Neste ponto, os dois arquivos necessários para a atividade estavam disponíveis no diretório.

---

## 6. Ocultação da mensagem na imagem

O `steghide` foi utilizado para incorporar `mensagem.txt` dentro da imagem:

```bash
steghide embed -cf Marcel_Proust_1895-cropped.jpg -ef mensagem.txt
```

Durante a execução, foi solicitada uma senha para proteger o conteúdo incorporado.

Saída:

```text
Enter passphrase: 
Re-Enter passphrase: 
embedding "mensagem.txt" in "Marcel_Proust_1895-cropped.jpg"... done
```

O comando utiliza:

* `embed` — indica que será realizado o processo de incorporação dos dados;
* `-cf` — **cover file**, arquivo de cobertura utilizado para esconder os dados;
* `-ef` — **embed file**, arquivo que será incorporado à imagem.

Após a operação, a própria imagem `Marcel_Proust_1895-cropped.jpg` passou a conter os dados ocultos.

---

## 7. Remoção do arquivo original

Para demonstrar a recuperação posterior da mensagem a partir da imagem, o arquivo original `mensagem.txt` foi removido:

```bash
rm mensagem.txt
```

Depois, foi verificado o conteúdo do diretório:

```bash
ls
```

Saída:

```text
Marcel_Proust_1895-cropped.jpg
```

Nesse momento, o arquivo de texto original não estava mais presente no diretório. A única cópia da mensagem estava incorporada à imagem.

---

## 8. Extração da mensagem oculta

Para recuperar o conteúdo escondido, foi utilizado:

```bash
steghide extract -sf Marcel_Proust_1895-cropped.jpg
```

Foi solicitada a senha utilizada durante o processo de incorporação.

Saída:

```text
Enter passphrase: 
wrote extracted data to "mensagem.txt".
```

O parâmetro utilizado foi:

* `-sf` — **stego file**, arquivo que contém os dados ocultos.

O `steghide` identificou os dados incorporados na imagem e recriou o arquivo `mensagem.txt`.

---

## 9. Verificação da mensagem recuperada

Após a extração, foi verificado o conteúdo do diretório:

```bash
ls
```

Saída:

```text
Marcel_Proust_1895-cropped.jpg  mensagem.txt
```

Em seguida, o conteúdo do arquivo recuperado foi exibido:

```bash
cat mensagem.txt
```

Saída:

```text
Hackers do bem com Esteganografia!
```

A mensagem original foi recuperada corretamente a partir da imagem, demonstrando o funcionamento da esteganografia utilizada no laboratório.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 9**, mostrando a presença do arquivo `mensagem.txt` após a extração e o conteúdo recuperado.

[**Evidências — Módulo 8 / Aulas 1 e 2**](../evidencias.pdf)
