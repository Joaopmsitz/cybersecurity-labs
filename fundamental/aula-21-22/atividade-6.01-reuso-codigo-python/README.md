# Atividade 6.1 — Reuso de Código em Python no Kali Linux

## Objetivo

Nesta atividade foi demonstrado o conceito de **reuso de código em Python** utilizando a biblioteca Pillow para realizar o processamento de uma imagem.

A prática consiste em baixar uma imagem para o Kali Linux, utilizar um código Python baseado em uma biblioteca já existente para redimensioná-la para `300x300` pixels e salvar o resultado em um novo arquivo.

O objetivo é compreender como componentes de software previamente desenvolvidos e testados podem ser reutilizados para implementar funcionalidades sem a necessidade de desenvolver toda a lógica de processamento de imagens do zero.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório utilizado:** `/home/aluno/Documentos/`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Preparação do ambiente

Antes das atividades do módulo, foi realizada a limpeza de arquivos de cache do `apt`, pacotes que não são mais necessários e logs antigos, conforme orientação do laboratório:

```bash
sudo apt clean
sudo apt autoremove
sudo journalctl --vacuum-time=1d
```

Esses comandos têm como objetivo liberar espaço na máquina virtual antes da realização das atividades.

---

## 2. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="u4c7m2"
sudo -i
```

Em seguida, foi acessado o diretório `Documentos`:

```bash id="p8x3n6"
cd /home/aluno/Documentos
```

Foi realizada uma verificação inicial do conteúdo do diretório:

```bash id="r5k9w1"
ls
```

---

## 3. Baixando a imagem

A imagem `My_shoe.jpg` foi baixada diretamente pelo terminal utilizando `wget`:

```bash id="k7m2v9"
wget https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
```

Saída observada no material do laboratório:

```text id="s6q1x8"
--2024-02-13 17:24:33--  https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 1297035 (1,2M) [image/jpeg]
Salvando em: “My_shoe.jpg”

My_shoe.jpg                 100%[==========================================>]   1,24M  --.-KB/s    em 0,1s    

2024-02-13 17:24:33 (8,28 MB/s) - “My_shoe.jpg” salvo [1297035/1297035]
```

Depois do download, foi executado:

```bash id="n3w7f5"
ls
```

Resultado:

```text id="d9q2m6"
My_shoe.jpg
```

Isso confirma que a imagem foi armazenada no diretório `/home/aluno/Documentos`.

---

## 4. Visualizando a imagem original

Com o arquivo disponível no sistema, foi aberto o **Thunar**, gerenciador de arquivos do Kali Linux.

A navegação foi realizada até:

```text
/home/aluno/Documentos
```

O arquivo `My_shoe.jpg` foi aberto para visualizar a imagem original.

Após a visualização, o visualizador de imagens foi fechado.

---

## 5. Criando o código Python

Foi aberto o editor de texto **Mousepad** e inserido o seguinte código:

```python
from PIL import Image

# Abre uma imagem existente
imagem_original = Image.open("My_shoe.jpg")

# Redimensiona a imagem para 300x300 pixels
imagem_redimensionada = imagem_original.resize((300, 300))

# Salva a imagem redimensionada
imagem_redimensionada.save("My_shoe_redimensionado.jpg")

# Fecha a imagem original
imagem_original.close()
```

O código utiliza a biblioteca **Pillow**, que fornece recursos para manipulação de imagens em Python.

### Importação da biblioteca

```python
from PIL import Image
```

Importa a classe `Image` da biblioteca Pillow.

A partir dela é possível realizar operações como abertura, redimensionamento e salvamento de imagens.

### Abertura da imagem

```python
imagem_original = Image.open("My_shoe.jpg")
```

A função `Image.open()` abre a imagem existente e atribui o objeto resultante à variável `imagem_original`.

### Redimensionamento

```python
imagem_redimensionada = imagem_original.resize((300, 300))
```

O método `resize()` cria uma nova versão da imagem com as dimensões:

```text
300 x 300 pixels
```

O resultado é armazenado em `imagem_redimensionada`.

### Salvamento

```python
imagem_redimensionada.save("My_shoe_redimensionado.jpg")
```

A imagem redimensionada é salva com o nome:

```text
My_shoe_redimensionado.jpg
```

### Fechamento

```python
imagem_original.close()
```

Fecha o arquivo da imagem original após a utilização.

O fechamento do recurso é uma boa prática para evitar manter arquivos ou recursos abertos desnecessariamente.

---

## 6. Salvando o script

O código foi salvo no diretório:

```text
/home/aluno/Documentos
```

com o nome:

```text
redimensionar_imagem.py
```

No Mousepad, foi necessário selecionar a opção **Todos os arquivos** no momento do salvamento para que o arquivo fosse criado com a extensão `.py`.

---

## 7. Executando o programa

Após fechar o Mousepad, o terminal foi utilizado para executar o script:

```bash id="v2k8r4"
python redimensionar_imagem.py
```

O script utiliza a imagem original como entrada e gera uma nova imagem redimensionada.

---

## 8. Verificando os arquivos gerados

Após a execução do programa, foi utilizado o comando:

```bash id="q5m9x1"
ls
```

Saída esperada no laboratório:

```text id="0w7c3p"
My_shoe.jpg  My_shoe_redimensionado.jpg  redimensionar_imagem.py
```

A saída demonstra que três arquivos estão presentes no diretório:

```text
My_shoe.jpg
My_shoe_redimensionado.jpg
redimensionar_imagem.py
```

O arquivo adicional `My_shoe_redimensionado.jpg` confirma que o script Python executou a operação de processamento da imagem e criou o novo arquivo.

**Este é o passo solicitado para a evidência da atividade.**

---

## Reuso de código

O conceito principal desta atividade é o **reuso de código**.

Em vez de implementar manualmente toda a lógica necessária para interpretar um arquivo JPEG, manipular pixels e gerar uma nova imagem, o programa utiliza funcionalidades fornecidas pela biblioteca Pillow.

A relação pode ser representada como:

```text
Python
   │
   ▼
Biblioteca Pillow
   │
   ├── Abrir imagem
   ├── Redimensionar imagem
   └── Salvar imagem
```

Dessa maneira, componentes já desenvolvidos podem ser incorporados a novos programas, reduzindo a quantidade de código necessário e permitindo que o desenvolvedor concentre seus esforços na lógica específica da aplicação.

---

## Resultado

A atividade demonstrou na prática o reuso de uma biblioteca Python para processamento de imagens.

O fluxo realizado foi:

```text
Baixar My_shoe.jpg
        ↓
Abrir imagem com Pillow
        ↓
Redimensionar para 300 x 300
        ↓
Salvar My_shoe_redimensionado.jpg
        ↓
Verificar arquivo criado
```

O arquivo `My_shoe_redimensionado.jpg` foi gerado a partir da imagem original utilizando o script `redimensionar_imagem.py`.

---

## Limpeza do ambiente

Após a conclusão da atividade, os arquivos utilizados foram removidos do diretório `Documentos`:

```bash id="h7p3m2"
rm *
```

O laboratório solicitou a confirmação da operação antes da remoção:

```text id="k4v8q6"
zsh: sure you want to delete all 3 files in /home/aluno/Documentos [yn]? y
```

Em seguida:

```bash id="n9c2w5"
ls
```

foi utilizado para confirmar o conteúdo final do diretório.

> O comando `rm *` é destrutivo e remove todos os arquivos correspondentes ao padrão no diretório atual. Em um ambiente real, é mais seguro verificar previamente o conteúdo e remover somente os arquivos necessários.

---

## Evidência

A evidência desta atividade corresponde ao **passo 8**, mostrando a listagem dos arquivos após a execução do script:

```text
My_shoe.jpg  My_shoe_redimensionado.jpg  redimensionar_imagem.py
```

[**Evidências — Módulo 6 / Aulas 1 e 2**](../evidencias.pdf)
