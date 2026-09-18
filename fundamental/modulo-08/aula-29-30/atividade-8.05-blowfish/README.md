# Atividade 8.5 — Cifrando e decifrando um arquivo com Blowfish no Linux

## Objetivo

Utilizar o **OpenSSL** para cifrar e decifrar um arquivo utilizando o algoritmo **Blowfish** no modo CFB, verificando na prática a criação de um arquivo cifrado e sua posterior recuperação.

A atividade também permite observar o comportamento do OpenSSL ao trabalhar com um algoritmo criptográfico considerado legado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Algoritmo:** Blowfish (BF-CFB)
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `CRS-20_Dragon–Enhanced.jpg`
* **Arquivo cifrado:** `arquivo_criptografado`
* **Arquivo recuperado:** `imagem.jpg`

> A senha utilizada durante o laboratório não é registrada neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash id="w7n3fc"
sudo -i
```

---

## 2. Acesso ao diretório de trabalho

Foi acessado o diretório utilizado na atividade:

```bash id="q5p2md"
cd /home/aluno/Documentos/Arquivos
```

---

## 3. Download da imagem

Foi utilizada uma imagem JPG obtida da Wikimedia Commons:

```bash id="n2x8va"
wget https://upload.wikimedia.org/wikipedia/commons/9/9e/CRS-20_Dragon%E2%80%93Enhanced.jpg
```

Saída registrada:

```text id="j3m8ks"
--2024-03-04 16:10:22--  https://upload.wikimedia.org/wikipedia/commons/9/9e/CRS-20_Dragon%E2%80%93Enhanced.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 2092509 (2,0M) [image/jpeg]
Salvando em: “CRS-20_Dragon–Enhanced.jpg”

CRS-20_Dragon–Enhanced.jpg     100%[===================================================>]   2,00M  10,6MB/s    em 0,2s    

2024-03-04 16:10:22 (10,6MB/s) - “CRS-20_Dragon–Enhanced.jpg” salvo [2092509/2092509]
```

A imagem foi aberta no **Thunar** para confirmar visualmente o arquivo antes da cifragem.

---

## 4. Cifragem utilizando Blowfish

Primeiramente, foi verificado o conteúdo do diretório:

```bash id="g4d6pw"
ls
```

Saída:

```text id="v2m7qn"
CRS-20_Dragon–Enhanced.jpg
```

Em seguida, foi utilizado o OpenSSL para cifrar a imagem:

```bash id="c8y4xr"
openssl enc -bf-cfb -salt -in CRS-20_Dragon–Enhanced.jpg -out arquivo_criptografado
```

Durante a operação, foi solicitada uma senha:

```text id="k2z9ht"
enter BF-CFB encryption password:
Verifying - enter BF-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Após a cifragem, o conteúdo do diretório foi novamente verificado:

```bash id="m8s4pc"
ls
```

Saída:

```text id="r5q1bv"
arquivo_criptografado  CRS-20_Dragon–Enhanced.jpg
```

### Parâmetros utilizados

* `enc` — utiliza a funcionalidade de cifragem de arquivos do OpenSSL;
* `-bf-cfb` — utiliza o algoritmo Blowfish no modo CFB;
* `-salt` — adiciona um salt ao processo de derivação da chave;
* `-in CRS-20_Dragon–Enhanced.jpg` — define a imagem original como entrada;
* `-out arquivo_criptografado` — define o arquivo cifrado como saída.

O OpenSSL também apresentou um aviso indicando que a derivação de chave utilizada é legada e recomendando o uso de `-iter` ou `-pbkdf2`.

---

## 5. Evidência da cifragem

A evidência solicitada para esta atividade corresponde ao **passo 5**, mostrando o arquivo original, a execução do comando de cifragem e a criação do arquivo cifrado:

```text id="b7f4mx"
ls
CRS-20_Dragon–Enhanced.jpg

openssl enc -bf-cfb -salt -in CRS-20_Dragon–Enhanced.jpg -out arquivo_criptografado
enter BF-CFB encryption password:
Verifying - enter BF-CFB encryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

ls 
arquivo_criptografado  CRS-20_Dragon–Enhanced.jpg
```

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)

---

## 6. Remoção do original e decifragem

Para verificar a recuperação do conteúdo, o arquivo original foi removido:

```bash id="p3w8za"
rm CRS-20_Dragon–Enhanced.jpg
```

Em seguida, o arquivo cifrado foi utilizado para realizar a decifragem:

```bash id="h6q2vt"
openssl enc -bf-cfb -d -in arquivo_criptografado -out imagem.jpg
```

Durante o processo, foi solicitada a senha utilizada anteriormente:

```text id="s4j9kc"
enter BF-CFB decryption password:
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
```

Após a decifragem, foi utilizado `ls`:

```bash id="d8m2qy"
ls
```

Resultado:

```text id="x5r7hn"
arquivo_criptografado  imagem.jpg
```

A imagem recuperada foi aberta no **Thunar** para verificar visualmente o resultado da decifragem.

---

## Observação técnica

O **Blowfish** é um algoritmo de cifragem simétrica de chave variável e hoje é considerado uma opção legada para novos projetos. A atividade demonstra seu funcionamento com o OpenSSL, mas algoritmos e modos mais modernos devem ser considerados em implementações atuais.

Também é importante observar que o comando utilizado no laboratório não especifica um tamanho de chave de 128 bits; o parâmetro `-bf-cfb` apenas seleciona o Blowfish no modo CFB.

Assim como nas atividades anteriores, o OpenSSL exibiu um aviso sobre a derivação de chave legada, recomendando mecanismos como `PBKDF2` para usos modernos.

---

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)
