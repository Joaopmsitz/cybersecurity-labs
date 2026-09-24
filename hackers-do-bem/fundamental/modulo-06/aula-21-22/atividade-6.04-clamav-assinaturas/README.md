# Atividade 6.4 — Conhecendo o Antivírus ClamAV e sua Assinatura de Malware no Kali Linux

## Objetivo

Nesta atividade foi realizada uma introdução ao **ClamAV**, antivírus de código aberto utilizado em sistemas Linux, com foco nas ferramentas `clambc` e `sigtool`.

O laboratório também abordou o funcionamento de assinaturas de malware e a identificação de vulnerabilidades associadas a assinaturas conhecidas, utilizando como exemplo a **CVE-2017-12099**.

A atividade teve caráter de análise e identificação. Não foi realizada a execução de malware.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="k4v8p2"
sudo -i
```

---

## 2. Conhecendo o `clambc`

O primeiro comando utilizado foi:

```bash id="m7x3q9"
clambc -h
```

O `clambc` é uma ferramenta do ClamAV destinada ao teste de **bytecode**, permitindo consultar e analisar assinaturas desse tipo.

A saída apresentada no laboratório foi:

```text id="r2n6w5"
                       Clam AntiVirus: Bytecode Testing Tool 1.4.3
           By The ClamAV Team: https://www.clamav.net/about.html#credits
           (C) 2024 Cisco Systems, Inc.

    clambc <file> [function] [param1 ...]

    --help                 -h         Show this help
    --version              -V         Show version
    --debug                           Show debug
    --force-interpreter    -f         Force using the interpreter instead of the JIT
    --trust-bytecode       -t         Trust loaded bytecode (default yes)
    --info                 -i         Print information about bytecode
    --printsrc             -p         Print bytecode source
    --printbcir            -c         Print IR of bytecode signature
    --input                -c         Input file to run the bytecode on
    --trace <level>        -T         Set bytecode trace level 0..7 (default 7)
    --no-trace-showsource  -s         Don't show source line during tracing
    --statistics=bytecode             Collect and print bytecode execution statistics
    file                              File to test

**Caution**: You should NEVER run bytecode signatures from untrusted sources.
Doing so may result in arbitrary code execution.
```

A própria ferramenta apresenta uma advertência importante: assinaturas de bytecode provenientes de fontes não confiáveis não devem ser executadas, pois isso pode resultar em execução arbitrária de código.

### Principais opções observadas

Algumas opções disponibilizadas pelo `clambc` incluem:

* `-h` — exibe a ajuda;
* `-V` — exibe a versão;
* `-i` — apresenta informações sobre bytecode;
* `-p` — exibe o código-fonte do bytecode;
* `-c` — exibe a representação intermediária da assinatura;
* `-T` — define o nível de rastreamento;
* `-f` — força o uso do interpretador em vez do JIT.

---

## 3. Conhecendo o `sigtool`

Em seguida, foi consultada a ajuda da ferramenta `sigtool`:

```bash id="v5q8k1"
sigtool -h
```

O `sigtool` é uma ferramenta do conjunto do ClamAV utilizada para trabalhar com assinaturas, bases de dados e informações relacionadas ao mecanismo de detecção.

Entre suas funcionalidades estão operações relacionadas à criação, análise e manipulação de assinaturas utilizadas pelo ClamAV.

A utilização da ferramenta permite compreender que a detecção de ameaças não depende apenas da existência de um arquivo malicioso isolado, mas também das informações e padrões utilizados pelo mecanismo de antivírus para identificar determinados artefatos.

---

## 4. Listando assinaturas de bytecode

Para consultar as assinaturas disponíveis, foi executado:

```bash id="c9m4x7"
sigtool --list-sigs
```

A saída apresentou diversas assinaturas relacionadas a exploits e outros tipos de ameaças.

Entre as entradas observadas estavam:

```text id="a6v2p8"
BC.Legacy.Exploit.CVE_2010_3333-5.{Exploit-CVE_2010_3333}
BC.Legacy.Exploit.CVE_2011_0090-1.{Exploit-CVE_2011_0090}
BC.Win.Packer.script2exe-6754169-0.{}
BC.Legacy.Exploit.CVE_2011_0086-1.{Exploit-CVE_2011_0086}
BC.Legacy.Exploit.CVE_2011_4373-2
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
...
```

A listagem demonstra que o ClamAV possui assinaturas associadas a diferentes categorias de ameaças, incluindo exploits identificados por **CVE (Common Vulnerabilities and Exposures)**.

---

## 5. Analisando a assinatura relacionada à CVE-2017-12099

Entre as assinaturas observadas estava:

```text id="u8q3m6"
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
```

A nomenclatura permite identificar alguns elementos:

```text id="y1r7k4"
BC
│
└── Bytecode

Img
│
└── relacionada a processamento de imagem

Exploit
│
└── indica uma assinatura associada a exploração

CVE_2017_12099
│
└── identificador da vulnerabilidade
```

A presença da CVE na assinatura permite relacionar a detecção do ClamAV com uma vulnerabilidade documentada externamente.

---

## 6. Identificando o tipo de ataque

Para a **CVE-2017-12099**, a atividade solicitou a consulta de referências sobre a vulnerabilidade e a identificação do tipo de ataque.

O ataque associado à vulnerabilidade foi identificado como:

```text id="p4w9n2"
Integer Overflow
```

**Este é o passo solicitado para a evidência da atividade.**

### Integer Overflow

Um **Integer Overflow** ocorre quando uma operação matemática produz um valor que ultrapassa o limite representável pelo tipo inteiro utilizado.

Em determinadas condições, isso pode provocar consequências de segurança quando o resultado é utilizado posteriormente em operações como:

* cálculo de tamanho;
* alocação de memória;
* processamento de arquivos;
* cópia de dados;
* validações de limites.

No contexto de uma vulnerabilidade, um cálculo incorreto causado por overflow pode contribuir para condições que permitam corrupção de memória ou outras formas de comportamento inesperado.

---

## 7. Relação entre CVE e assinatura do antivírus

A atividade demonstra uma relação importante entre bases de vulnerabilidades e mecanismos de detecção.

A **CVE** fornece uma identificação padronizada para uma vulnerabilidade conhecida, enquanto uma assinatura do ClamAV pode ser criada para detectar artefatos associados a uma determinada ameaça ou exploração.

No caso observado:

```text id="n3v6q1"
CVE-2017-12099
        │
        ▼
Vulnerabilidade documentada
        │
        ▼
Exploit associado
        │
        ▼
Assinatura do ClamAV
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
```

Isso permite que analistas relacionem informações de vulnerabilidades, ameaças e mecanismos de detecção durante uma investigação.

---

## 8. Pesquisa de outros exploits

Como parte da atividade, foram pesquisadas outras assinaturas e vulnerabilidades identificadas por CVE.

A própria saída do:

```bash id="e7k5r3"
sigtool --list-sigs
```

apresentou exemplos como:

```text id="q2w8m5"
BC.Legacy.Exploit.CVE_2010_3333-5.{Exploit-CVE_2010_3333}
BC.Legacy.Exploit.CVE_2011_0090-1.{Exploit-CVE_2011_0090}
BC.Legacy.Exploit.CVE_2011_0086-1.{Exploit-CVE_2011_0086}
BC.Legacy.Exploit.CVE_2011_4373-2
```

Esses identificadores mostram como diferentes vulnerabilidades podem aparecer associadas a assinaturas específicas.

A utilização de CVEs como referência também facilita a correlação entre ferramentas de segurança, bases públicas de vulnerabilidades e informações de pesquisa.

---

## Conceitos envolvidos

### ClamAV

O **ClamAV** é um mecanismo antivírus de código aberto utilizado principalmente em sistemas Unix/Linux.

Ele utiliza diferentes tipos de assinaturas e mecanismos de análise para identificar arquivos e conteúdos associados a ameaças conhecidas.

### Assinatura de malware

Uma assinatura representa informações utilizadas para reconhecer determinados padrões associados a uma ameaça.

No contexto do ClamAV, assinaturas podem estar relacionadas a diferentes categorias de arquivos, exploits e outros artefatos.

### Bytecode

Bytecode é uma forma de código intermediário que pode ser utilizada pelo mecanismo do ClamAV para implementar determinadas verificações.

O `clambc` fornece recursos específicos para testar e analisar assinaturas desse tipo.

### CVE

**CVE (Common Vulnerabilities and Exposures)** é um sistema utilizado para identificar vulnerabilidades de segurança publicamente conhecidas.

Exemplo utilizado nesta atividade:

```text
CVE-2017-12099
```

### Integer Overflow

É uma condição na qual um cálculo inteiro ultrapassa o limite representável pelo tipo utilizado.

Em segurança da informação, esse tipo de erro pode se tornar relevante quando o valor resultante influencia operações de memória, tamanho ou processamento de dados.

---

## Resultado

A atividade permitiu explorar ferramentas do ClamAV relacionadas a assinaturas e bytecode.

Foram realizados:

1. acesso administrativo ao Kali Linux;
2. consulta da ajuda do `clambc`;
3. consulta da ajuda do `sigtool`;
4. listagem das assinaturas disponíveis;
5. identificação de assinaturas relacionadas a CVEs;
6. identificação da assinatura relacionada à `CVE-2017-12099`;
7. pesquisa da vulnerabilidade;
8. identificação do tipo de ataque como **Integer Overflow**;
9. pesquisa de outros exploits referenciados por CVE.

O exercício também demonstrou como uma ferramenta de antivírus pode relacionar assinaturas de detecção com vulnerabilidades e exploits conhecidos.

---

## Evidência

A evidência desta atividade corresponde ao **passo 6**, contendo a identificação do tipo de ataque associado à `CVE-2017-12099`.

[**Evidências — Módulo 6 / Aulas 1 e 2**](../evidencias.pdf)
