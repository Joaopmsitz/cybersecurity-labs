# Atividade 2.2 — Explorando o Keylogger XSPY no Kali Linux

## Objetivo

Explorar, em um ambiente controlado de laboratório, o funcionamento do **Keylogger XSPY** no Kali Linux.

A atividade teve como objetivo observar como um keylogger pode monitorar as teclas digitadas durante sua execução e armazenar os dados capturados em um arquivo de texto.

> **Aviso:** a atividade foi realizada exclusivamente para fins acadêmicos, dentro do ambiente de laboratório. O keylogger foi utilizado somente para demonstrar seu funcionamento e não foi empregado para capturar informações de terceiros.

## Ambiente

* Kali Linux
* Terminal
* XSPY
* Editor de texto
* Sistema virtualizado de laboratório

## Procedimento

### 1. Acesso ao diretório de documentos

O Terminal foi aberto e o diretório `Documentos` foi acessado:

```bash
cd /home/aluno/Documentos
```

Em seguida, foi utilizado o comando `ls` para verificar o conteúdo do diretório:

```bash
ls
```

Como o diretório estava sendo utilizado para armazenar o resultado da atividade, inicialmente não havia o arquivo `teste.log`.

### 2. Inicialização do XSPY

O XSPY foi iniciado no Terminal com seu resultado sendo redirecionado para o arquivo `teste.log`:

```bash
xspy >> teste.log
```

O operador `>>` foi utilizado para direcionar a saída do programa para um arquivo de texto.

A partir desse momento, o XSPY passou a registrar as teclas utilizadas durante a demonstração.

### 3. Digitação de texto para teste

Com o XSPY em execução, foi aberto o editor de texto do Kali Linux.

Foi digitada manualmente a seguinte frase:

```text
Hacker do bem!
```

A digitação foi realizada diretamente pelo teclado, sem utilizar copiar e colar, permitindo que o keylogger registrasse os eventos de teclado.

### 4. Encerramento do XSPY

Após a digitação do texto de teste, o Terminal foi acessado novamente e a execução do XSPY foi interrompida utilizando:

```text
Ctrl + C
```

O Terminal apresentou o encerramento da execução:

```text
xspy >> teste.log
^C
```

### 5. Verificação do arquivo de captura

Após o encerramento do programa, foi utilizado o comando `ls` para verificar se o arquivo havia sido criado:

```bash
ls
```

O resultado observado foi:

```text
teste.log
```

A presença do arquivo confirmou que a saída do XSPY havia sido armazenada no diretório `Documentos`.

### 6. Visualização dos dados capturados

Para visualizar o conteúdo do arquivo, foi utilizado:

```bash
cat teste.log
```

A saída observada no ambiente de laboratório foi semelhante a:

```text
opened :10.0 for snoopng

Shift_L hacker do bemShift_L 1Control_L c
```

A saída não reproduziu necessariamente o texto exatamente da mesma forma que foi digitado. Isso ocorre devido à forma como os eventos de teclado são capturados no ambiente virtualizado utilizado na atividade.

Mesmo assim, foi possível identificar na saída a sequência correspondente à frase digitada:

```text
hacker do bem
```

Também foram registrados eventos relacionados às teclas utilizadas durante a atividade, como `Shift_L` e `Control_L`.

Esse resultado demonstrou que o XSPY consegue registrar eventos de teclado e armazená-los em um arquivo para posterior consulta.

### 7. Remoção do arquivo

Após a análise do conteúdo capturado, o arquivo de teste foi removido:

```bash
rm teste.log
```

Em seguida, o diretório foi novamente verificado:

```bash
ls
```

O arquivo `teste.log` não estava mais presente no diretório.

A remoção foi realizada para não deixar dados capturados pelo experimento no ambiente de laboratório.

## Comandos utilizados

Os comandos utilizados durante a atividade foram:

```bash
cd /home/aluno/Documentos
ls
xspy >> teste.log
```

Após a execução do keylogger:

```text
Ctrl + C
```

Para verificar o arquivo criado:

```bash
ls
```

Para visualizar os dados registrados:

```bash
cat teste.log
```

E, finalmente, para remover o arquivo:

```bash
rm teste.log
ls
```

## Interpretação

O experimento demonstrou o funcionamento básico de um **keylogger**, que é um tipo de software capaz de registrar eventos de teclado.

O fluxo observado foi:

```text
Teclado
   │
   ▼
XSPY
   │
   ▼
teste.log
   │
   ▼
cat teste.log
   │
   ▼
Visualização dos eventos capturados
```

O redirecionamento utilizado no comando:

```bash
xspy >> teste.log
```

permitiu armazenar a saída do programa em um arquivo.

A consulta posterior com `cat` demonstrou que as informações registradas durante a execução permaneceram armazenadas no arquivo mesmo após o encerramento do XSPY.

O laboratório também mostrou que a representação dos dados capturados pode variar de acordo com o ambiente. No caso da VM utilizada, alguns eventos foram apresentados com seus nomes de teclas, como `Shift_L` e `Control_L`.

## Resultado

Foi possível:

* Acessar o diretório utilizado para armazenar os dados da atividade;
* Inicializar o XSPY;
* Criar o arquivo `teste.log`;
* Realizar uma digitação controlada para teste;
* Encerrar o keylogger com `Ctrl + C`;
* Confirmar a criação do arquivo com `ls`;
* Visualizar os eventos registrados utilizando `cat`;
* Identificar a frase digitada na saída capturada;
* Remover o arquivo após a conclusão do experimento.

A atividade demonstrou, de forma controlada, como um keylogger pode registrar eventos de teclado e armazenar os dados capturados para posterior análise.

## Conceitos praticados

* Keylogger
* XSPY
* Captura de teclas
* Eventos de teclado
* Redirecionamento de saída
* Arquivos de log
* `>>`
* `ls`
* `cat`
* `rm`
* Monitoramento de entrada
* Segurança de endpoints

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 05–06.

[Ver evidências — Aula 05–06](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-05-06/evidencias.pdf)
