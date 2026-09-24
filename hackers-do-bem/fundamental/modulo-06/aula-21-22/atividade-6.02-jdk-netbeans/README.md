# Atividade 6.2 — Conhecendo o SDK do Java (JDK) e um IDE no Kali Linux

## Objetivo

Nesta atividade foi realizada a instalação e verificação do ambiente de desenvolvimento Java no Kali Linux, utilizando o **Java Development Kit (JDK)** e o **Apache NetBeans** como IDE.

O exercício demonstra a relação entre o JDK, responsável por fornecer as ferramentas necessárias para desenvolvimento Java, e uma IDE, que oferece um ambiente integrado para criação e desenvolvimento de aplicações.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório do NetBeans:** `/curso/netbeans`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="n4x7p2"
sudo -i
```

O acesso administrativo foi utilizado para realizar a verificação e instalação do pacote do Apache NetBeans.

---

## 2. Verificando o JDK

O laboratório já disponibilizava o JDK instalado. Para verificar a versão disponível, foi executado:

```bash id="q8m3v6"
java --version
```

Saída observada:

```text id="7k2p9x"
openjdk 23-ea 2024-09-17
OpenJDK Runtime Environment (build 23-ea+20-Debian-1)
OpenJDK 64-Bit Server VM (build 23-ea+20-Debian-1, mixed mode, sharing)
```

A saída confirma que o ambiente possui uma versão do **OpenJDK** disponível para utilização.

### OpenJDK

O OpenJDK é uma implementação de código aberto da plataforma Java.

A instalação do JDK fornece componentes necessários para desenvolvimento Java, incluindo ferramentas utilizadas para compilar e executar aplicações.

A versão observada no laboratório foi:

```text
OpenJDK 23-ea
```

---

## 3. Acessando o diretório do NetBeans

O pacote do Apache NetBeans utilizado na atividade estava armazenado no diretório:

```text id="x6r1m8"
/curso/netbeans
```

Foi utilizado:

```bash id="m9v4q2"
cd /curso/netbeans
```

---

## 4. Verificando o pacote de instalação

Após acessar o diretório, foi executado:

```bash id="w5k8n3"
ls
```

Saída observada:

```text id="c2x7m9"
apache-netbeans_19-1_all.deb
```

O arquivo `.deb` corresponde ao pacote utilizado para instalação do Apache NetBeans no sistema.

O formato `.deb` é utilizado em distribuições baseadas em Debian, como o Kali Linux.

---

## 5. Instalando o Apache NetBeans

A instalação foi realizada utilizando o `dpkg`:

```bash id="f8q3v1"
dpkg -i apache-netbeans_19-1_all.deb
```

Saída observada:

```text id="2m7x5q"
Selecionando pacote previamente não selecionado apache-netbeans.
(Lendo banco de dados ... 364754 arquivos e diretórios atualmente instalados).
Preparando para desempacotar apache-netbeans_19-1_all.deb ...
Desempacotando apache-netbeans (19-1) ...
Configurando apache-netbeans (19-1) ...
Processando gatilhos para kali-menu (2025.3.2) ...
Processando gatilhos para desktop-file-utils (0.28-1) ...
Processando gatilhos para hicolor-icon-theme (0.18-2) ...
```

A saída indica as principais etapas realizadas pelo `dpkg`:

1. identificação do pacote;
2. preparação do pacote para instalação;
3. desempacotamento dos arquivos;
4. configuração do Apache NetBeans;
5. processamento dos gatilhos relacionados ao menu do Kali;
6. atualização dos arquivos de desktop;
7. processamento dos ícones do sistema.

---

## 6. Abrindo o Apache NetBeans

Após a instalação, o Apache NetBeans foi iniciado através do menu do Kali Linux:

```text id="r6k1v4"
Aplicativos
└── Aplicativos habituais
    └── Desenvolvimento
        └── Apache NetBeans
```

A aplicação foi aberta para verificar o funcionamento da IDE.

---

## 7. Explorando o NetBeans

Com o Apache NetBeans aberto, foi possível visualizar o ambiente integrado de desenvolvimento.

O NetBeans é uma **IDE (Integrated Development Environment)**, ou Ambiente Integrado de Desenvolvimento.

Uma IDE reúne em uma única aplicação ferramentas que auxiliam no desenvolvimento de software, como:

* edição de código;
* organização de projetos;
* execução de aplicações;
* depuração;
* gerenciamento de arquivos;
* integração com ferramentas de desenvolvimento.

**Este é o passo solicitado para a evidência da atividade.**

---

## Conceitos envolvidos

### JDK — Java Development Kit

O **JDK** é o kit de desenvolvimento utilizado para criar aplicações Java.

Ele fornece ferramentas necessárias para trabalhar com o ecossistema Java, incluindo componentes utilizados na compilação e execução de programas.

Na atividade, a disponibilidade do JDK foi confirmada através de:

```bash id="b7m2x8"
java --version
```

Resultado:

```text id="9k4v1p"
openjdk 23-ea 2024-09-17
```

### IDE — Integrated Development Environment

Uma IDE fornece um ambiente integrado para desenvolvimento de software.

Em vez de utilizar diferentes ferramentas separadas para editar, executar e organizar o código, o desenvolvedor pode realizar essas tarefas dentro de uma única aplicação.

### Apache NetBeans

O Apache NetBeans é uma IDE que oferece suporte ao desenvolvimento de aplicações, incluindo projetos Java.

Nesta atividade, ele foi instalado através do pacote:

```text id="c5x9m3"
apache-netbeans_19-1_all.deb
```

utilizando:

```bash id="w2k7q4"
dpkg -i apache-netbeans_19-1_all.deb
```

### dpkg

O `dpkg` é uma ferramenta de baixo nível utilizada para instalação, remoção e gerenciamento de pacotes `.deb` em sistemas baseados em Debian.

Na atividade:

```bash id="p3v8n6"
dpkg -i apache-netbeans_19-1_all.deb
```

foi utilizado para instalar o pacote local do Apache NetBeans.

---

## Relação entre JDK e IDE

O JDK e o NetBeans possuem funções diferentes, mas complementares:

```text id="x4q8m1"
JDK
 │
 ├── Ferramentas da plataforma Java
 ├── Compilação
 └── Execução
       │
       ▼
Apache NetBeans
 │
 ├── Editor
 ├── Projetos
 ├── Execução
 └── Ferramentas de desenvolvimento
```

O JDK fornece a base necessária para trabalhar com Java, enquanto a IDE disponibiliza uma interface integrada para facilitar o desenvolvimento.

---

## Resultado

A atividade confirmou a disponibilidade do JDK no Kali Linux e realizou a instalação do Apache NetBeans através de um pacote `.deb`.

O JDK foi verificado com:

```bash id="j6m2w9"
java --version
```

e o pacote do NetBeans foi instalado com:

```bash id="r8x4p3"
dpkg -i apache-netbeans_19-1_all.deb
```

Após a instalação, o Apache NetBeans foi aberto e explorado, confirmando a disponibilidade do ambiente de desenvolvimento no sistema.

---

## Evidência

A evidência desta atividade corresponde ao **passo 7**, mostrando o Apache NetBeans aberto após a instalação e permitindo visualizar a interface da IDE.

[**Evidências — Módulo 6 / Aulas 1 e 2**](../evidencias.pdf)
