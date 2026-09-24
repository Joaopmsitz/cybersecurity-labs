# Atividade 2.3 — Explorando Ransomwares no Kali Linux

## Objetivo

Explorar, em um ambiente controlado de laboratório, uma ferramenta capaz de gerar amostras de ransomware no Kali Linux.

A atividade teve como objetivo compreender a existência de diferentes famílias de ransomware, observar o processo de geração de uma amostra e verificar o artefato criado no sistema de arquivos.

O ransomware gerado durante o laboratório **não foi executado**. A atividade foi limitada à criação e inspeção do arquivo para fins educacionais.

> **Aviso:** ransomware é um tipo de malware capaz de causar indisponibilidade e perda de dados. O artefato criado nesta atividade não deve ser executado fora de um ambiente de análise controlado.

## Ambiente

* Kali Linux
* Terminal
* Ransomware Creator
* Python 3
* Thunar
* Sistema virtualizado de laboratório

## Procedimento

### 1. Acesso ao modo administrador

O Terminal foi aberto e o ambiente foi acessado com privilégios administrativos:

```bash id="jv3x6k"
sudo -i
```

### 2. Acesso ao diretório da ferramenta

Em seguida, foi acessado o diretório onde a ferramenta de criação de ransomware estava disponibilizada:

```bash id="4z5q81"
cd /curso/Ransomware
```

A ferramenta foi executada com Python 3:

```bash id="m9w1f2"
python3 Ransomware
```

Após a inicialização, foi apresentada a interface do programa:

```text id="0h2p8q"
██████╗  █████╗ ███╗   ██╗███████╗ ██████╗ ███╗   ███╗
██╔══██╗██╔══██╗████╗  ██║██╔════╝██╔══██╗████╗ ████║
██████╔╝███████║██╔██╗ ██║███████╗██║   ██║██╔████╔██║
██╔══██╗██╔══██║██║╚██╗██║╚════██║██║   ██║██║╚██╔╝██║
██║  ██║██║  ██║██║ ╚████║███████║╚██████╔╝██║ ╚═╝ ██║
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝╚══════╝ ╚═════╝ ╚═╝     ╚═╝

           RANSOMWARE CREATOR BY ERR0R

Ransomware Virus Creator Tools Version 1.0
DON'T Try to Use it on Your Computer!
```

### 3. Exploração dos comandos disponíveis

Foi utilizado o comando:

```text id="w3m5jx"
Ransomware®Creator~> help
```

A ferramenta apresentou as opções disponíveis:

```text id="xj6b1p"
----------------------------------
| Commands            Description|
----------------------------------
| Help                How to Use |
| Show      Show List Ransomware |
| Clear             Clear window |
| Menu              Back to Menu |
| EXIT              Exit Program |
----------------------------------
```

O comando `help` permitiu identificar as operações básicas disponibilizadas pela ferramenta.

### 4. Listagem das famílias disponíveis

Para visualizar as amostras disponíveis para criação, foi utilizado:

```text id="5b7v4c"
Ransomware®Creator~> show
```

A ferramenta apresentou:

```text id="8x4f2d"
This Files are Very Sensitive
Be Careful While You Using Them !

01. Ransomware.Cerber
02. Ransomware.Cryptowall
03. Ransomware.Jigsaw
04. Ransomware.Locky
05. Ransomware.Mamba
06. Ransomware.Matsnu
07. Ransomware.Petrwrap
08. Ransomware.Petya
09. Ransomware.Radamant
10. Ransomware.Rex
11. Ransomware.Satana
12. Ransomware.TeslaCrypt
13. Ransomware.Vipasana
14. Ransomware.WannaCry
15. Ransomware.WannaCry_Plus
```

A listagem permitiu observar que a ferramenta disponibiliza referências a diferentes famílias de ransomware.

### 5. Verificação do diretório raiz

Um segundo Terminal foi utilizado para acompanhar a criação do artefato no sistema de arquivos.

O diretório raiz foi acessado:

```bash id="xv6p3n"
cd /
```

Em seguida:

```bash id="r1k7sz"
ls
```

Antes da geração do artefato, a saída apresentava os diretórios padrão do sistema:

```text id="z0q5mj"
bin   curso  etc   lib   lost+found  mnt  proc  run   snap  sys  usr
boot  dev    home  lib64 media       opt  root  sbin  srv   tmp  var
```

Essa etapa serviu como referência para identificar posteriormente a criação do novo arquivo/diretório utilizado pela ferramenta.

### 6. Geração da amostra WannaCry

De volta ao primeiro Terminal, foi selecionada a opção correspondente à amostra WannaCry:

```text id="6k2s9a"
Ransomware®Creator~> 14
```

A ferramenta iniciou o processo de geração e apresentou:

```text id="m5w8x1"
Creating Ransomware
File name: Ransomware.WannaCry.zip
File type: .zip

[+] Loading... 100 % [success]

Completed
File saved as /sdcard
For back to main menu, type: menu
```

O resultado indica que a ferramenta concluiu a geração do artefato e o salvou no caminho:

```text id="n7c4qx"
/sdcard
```

O arquivo foi tratado somente como **artefato de análise** e não foi executado.

### 7. Verificação da criação do artefato

No segundo Terminal, o comando `ls` foi executado novamente:

```bash id="4b2z7k"
ls
```

A nova saída apresentou o diretório `sdcard`:

```text id="8qf3yc"
bin   curso  etc   lib   lost+found  mnt  proc  run   sdcard  srv  tmp  var
boot  dev    home  lib64  media       opt  root  sbin  snap    sys  usr
```

A presença de `sdcard` confirmou que a ferramenta havia criado o artefato no sistema de arquivos.

### 8. Inspeção do arquivo pelo Thunar

O explorador de arquivos **Thunar** foi aberto para realizar uma inspeção visual do conteúdo.

O caminho utilizado foi:

```text id="d4v8kp"
/
```

Dentro do diretório raiz, foi localizado o arquivo:

```text id="q5s2mn"
sdcard
```

O arquivo foi aberto para visualizar seu conteúdo.

### 9. Identificação do executável

Dentro do `sdcard`, foi identificado um arquivo com extensão `.exe`, com aproximadamente **3,5 MB**.

O artefato correspondia ao executável associado à amostra WannaCry gerada pela ferramenta.

Essa foi a etapa utilizada como evidência da atividade, pois permitiu visualizar diretamente que a ferramenta havia produzido um executável.

> **Importante:** o executável foi somente identificado e inspecionado. Ele não foi aberto nem executado.

## Comandos utilizados

Os principais comandos utilizados durante a atividade foram:

```bash id="v7c9x2"
sudo -i
cd /curso/Ransomware
python3 Ransomware
```

Para acompanhar o sistema de arquivos:

```bash id="h2p6nm"
cd /
ls
```

Após a geração da amostra, o comando `ls` foi utilizado novamente para confirmar a criação de:

```text id="q9r4tw"
sdcard
```

## Interpretação

O laboratório demonstrou uma etapa importante do ciclo de uma ameaça de ransomware: a geração de um artefato que posteriormente poderia ser utilizado para comprometer um sistema.

A ferramenta disponibilizada no laboratório apresentou uma lista contendo referências a diversas famílias de ransomware. A opção escolhida gerou uma amostra associada ao **WannaCry**.

O fluxo observado foi:

```text id="8p6z1k"
Ransomware Creator
        │
        ▼
Seleção da amostra
        │
        ▼
Geração do artefato
        │
        ▼
/sdcard
        │
        ▼
Inspeção no Thunar
        │
        ▼
Executável identificado
```

A atividade também reforçou a diferença entre **criar/observar um artefato de malware** e **executá-lo**. Neste laboratório, a análise foi encerrada antes de qualquer execução, reduzindo o risco de alteração ou indisponibilidade do ambiente.

## Resultado

Foi possível:

* Inicializar a ferramenta Ransomware Creator;
* Consultar os comandos disponíveis com `help`;
* Listar diferentes famílias de ransomware com `show`;
* Selecionar a amostra associada ao WannaCry;
* Gerar o artefato dentro do ambiente controlado;
* Confirmar sua criação utilizando `ls`;
* Localizar o arquivo `sdcard` no diretório raiz;
* Inspecionar o conteúdo utilizando o Thunar;
* Identificar um executável `.exe` de aproximadamente 3,5 MB;
* Encerrar a atividade sem executar o ransomware;
* Remover o artefato ao final do laboratório.

A atividade permitiu compreender, de forma prática e controlada, como ferramentas maliciosas podem gerar artefatos executáveis e por que esses arquivos devem ser tratados como potencialmente perigosos.

## Conceitos praticados

* Ransomware
* Malware
* WannaCry
* Ransomware Creator
* Artefato malicioso
* Executável Windows
* Análise de malware
* Sistema de arquivos Linux
* Inspeção de arquivos
* Ambiente controlado
* Segurança de endpoints
* Prevenção contra execução de malware

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 05–06.

[Ver evidências — Aula 05–06](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-05-06/evidencias.pdf)
