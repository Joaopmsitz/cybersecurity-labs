# Atividade 8.4 — Cifrando e decifrando um arquivo com 3DES no Linux

## Objetivo

Utilizar o **OpenSSL** para cifrar e decifrar um arquivo utilizando **3DES (Triple DES)** no modo CFB, verificando na prática a criação do arquivo cifrado e sua posterior recuperação.

A atividade também permite observar o comportamento do OpenSSL ao utilizar um algoritmo criptográfico considerado **legado**.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo:** 3DES / DES-EDE3-CFB
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `Hyla_japonica_sep01.jpg`
* **Arquivo cifrado:** `arquivo_criptografado`
* **Arquivo recuperado:** `imagem.jpg`

> A senha utilizada durante o laboratório não é registrada neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash id="c9rj4h"
sudo -i
```

---

## 2. Acesso ao diretório de trabalho

Foi acessado o diretório utilizado para armazenar os arquivos da atividade:

```bash id="r6j3s8"
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Download da imagem

Foi utilizada uma imagem JPG obtida da Wikimedia Commons:

```bash id="v4q2ny"
wget https://upload.wikimedia.org/wikipedia/commons/5/5a/Hyla_japonica_sep01.jpg
```

Saída registrada no laboratório:

```text id="m0c4jx"
--2024-03-03 20:56:15--  https://upload.wikimedia.org/wikipedia/commons/5/5a/Hyla_japonica_sep01.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 2900468 (2,8M) [image/jpeg]
Salvando em: “Hyla_japonica_sep01.jpg”

Hyla_japonica_sep01.jpg        100%[===================================================>]   2,77M  12,7MB/s    em 0,2s    

2024-03-03 20:56:15 (12,7MB/s) - “Hyla_japonica_sep01.jpg” salvo [2900468/2900468]
```

A imagem foi aberta no **Thunar** para verificar o arquivo antes da cifragem.

---

## 4. Cifragem utilizando 3DES

Foi realizada a verificação inicial do arquivo:

```bash id="xj5xgk"
ls
```

Saída:

```text id="q6z7gk"
Hyla_japonica_sep01.jpg
```

Em seguida, o arquivo foi cifrado com o OpenSSL:

```bash id="x4eq8w"
openssl enc -des-ede3-cfb -salt -in Hyla_japonica_sep01.jpg -out arquivo_criptografado
```

Durante a operação, foi solicitada uma senha:

```text id="7g0f2p"
enter DES-EDE3-CFB encryption password:
Verifying - enter DES-EDE3-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Após a cifragem, foi executado novamente:

```bash id="a2a4k8"
ls
```

Resultado:

```text id="x9s1ae"
arquivo_criptografado  Hyla_japonica_sep01.jpg
```

### Parâmetros utilizados

* `enc` — utiliza a funcionalidade de cifragem de arquivos do OpenSSL;
* `-des-ede3-cfb` — utiliza Triple DES (3DES), também identificado pelo algoritmo `DES-EDE3`, no modo CFB;
* `-salt` — adiciona um salt ao processo de derivação da chave;
* `-in Hyla_japonica_sep01.jpg` — define a imagem original como entrada;
* `-out arquivo_criptografado` — define o arquivo cifrado como saída.

O OpenSSL apresentou o aviso sobre o uso de uma derivação de chave considerada legada, recomendando `-iter` ou `-pbkdf2` para usos modernos.

---

## 5. Evidência da cifragem

A evidência solicitada para esta atividade corresponde ao **passo 5**, contendo a verificação do arquivo original, a execução da cifragem e a confirmação da criação do arquivo cifrado:

```text id="j9v3r5"
ls
Hyla_japonica_sep01.jpg

openssl enc -des-ede3-cfb -salt -in Hyla_japonica_sep01.jpg -out arquivo_criptografado
enter DES-EDE3-CFB encryption password:
Verifying - enter DES-EDE3-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls
arquivo_criptografado  Hyla_japonica_sep01.jpg
```

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)

---

## 6. Decifragem do arquivo

Após confirmar a criação do arquivo cifrado, o arquivo original foi removido:

```bash id="4q8y3b"
rm Hyla_japonica_sep01.jpg
```

Em seguida, o arquivo cifrado foi decifrado:

```bash id="6k8j8m"
openssl enc -des-ede3-cfb -d -in arquivo_criptografado -out imagem.jpg
```

Durante o processo, foi solicitada a senha utilizada na cifragem:

```text id="n1q2as"
enter DES-EDE3-CFB decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Por fim, foi utilizado `ls` para verificar o arquivo recuperado:

```bash id="t6r3w1"
ls
```

Saída:

```text id="z7x4c2"
arquivo_criptografado  imagem.jpg
```

A imagem recuperada foi aberta no **Thunar** para verificar visualmente o resultado da decifragem.

---

## Observação técnica

O **3DES** é um algoritmo criptográfico legado. A atividade demonstra seu funcionamento por meio do OpenSSL, mas sua utilização não representa a escolha recomendada para projetos novos. Em sistemas modernos, algoritmos mais atuais devem ser considerados conforme o caso de uso e os requisitos de segurança.

Além disso, o comando utilizado no laboratório gera o aviso referente à derivação de chave legada. O próprio OpenSSL recomenda mecanismos como `PBKDF2` para melhorar esse processo.

---

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)
