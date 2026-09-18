# Atividade 1.9 — Realizando OSINT com Maltego

## Objetivo

Utilizar o **Maltego** para realizar uma atividade de **OSINT (Open Source Intelligence)**, partindo de um domínio público e utilizando diferentes *Transforms* para identificar informações relacionadas à infraestrutura, DNS, pessoas, endereços de e-mail e servidores de e-mail.

A atividade foi realizada de forma passiva, utilizando informações públicas associadas ao domínio analisado.

## Ambiente

* Kali Linux
* Terminal
* Maltego
* Firefox
* Internet
* Domínio analisado: `ufc.br`

## Procedimento

### 1. Inicialização do Maltego

O Maltego foi iniciado pelo Terminal utilizando:

```bash
maltego
```

Após a abertura da aplicação, foi criado um novo projeto para realizar a análise.

### 2. Adição do domínio ao projeto

Na área **Entity Palette**, foi localizada a entidade:

```text
Infrastructure → Website
```

A entidade **Website** foi arrastada para o canvas.

Inicialmente, o Maltego apresentou o domínio:

```text
www.maltego.com
```

Esse valor foi alterado para:

```text
ufc.br
```

Durante a alteração, foi apresentada uma solicitação relacionada ao certificado de confiança. A opção de cancelamento foi utilizada para prosseguir com a atividade.

### 3. Consulta de domínios relacionados

Com a entidade `ufc.br` adicionada ao canvas, foi aberto o menu de contexto através do botão direito.

Foi acessado:

```text
+ All Transforms
```

E executado o Transform:

```text
[Utilities] To Domains [within Properties]
```

Esse procedimento permitiu consultar informações relacionadas aos domínios presentes nas propriedades da entidade analisada.

O resultado foi adicionado ao gráfico do Maltego para continuar a investigação.

### 4. Consulta de registros DNS

Em seguida, foi utilizado novamente o menu:

```text
+ All Transforms
```

Foi executado:

```text
[Utilities] To DNSNames [within Properties]
```

O Transform permitiu obter nomes relacionados ao DNS a partir das informações disponíveis na entidade.

Essa etapa demonstrou como informações públicas de DNS podem ser utilizadas para ampliar o contexto de uma investigação de OSINT.

### 5. Identificação de pessoas relacionadas

Sobre a entidade `ufc.br`, foi acessado novamente o menu de Transformações.

Foi utilizado:

```text
[Utilities] To Person [PGP]
```

O Transform realizou uma busca por possíveis pessoas relacionadas ao domínio através de informações disponíveis em registros PGP públicos.

As entidades retornadas foram apresentadas no gráfico do Maltego.

### 6. Identificação de endereços de e-mail

Também foi executado o Transform:

```text
[Utilities] To Email Addresses [PGP]
```

A consulta teve como objetivo identificar endereços de e-mail associados às informações públicas encontradas através do PGP.

Os resultados foram apresentados como novas entidades no gráfico.

Essa etapa demonstra como informações aparentemente separadas podem ser relacionadas durante uma investigação de OSINT.

### 7. Identificação dos servidores de e-mail

Por fim, foi utilizado o Transform:

```text
[Utilities] To DNS Name - MX (mail server)
```

O objetivo foi identificar os servidores responsáveis pelo recebimento de e-mails do domínio.

O resultado apresentou servidores de e-mail associados ao domínio analisado. Durante a atividade, os servidores apresentados estavam relacionados à infraestrutura do **Google**.

Registros **MX (Mail Exchange)** são utilizados pelo DNS para indicar quais servidores devem receber mensagens destinadas a um determinado domínio.

### 8. Análise do gráfico

Após a execução dos Transforms, o Maltego apresentou diferentes entidades relacionadas ao domínio `ufc.br`.

A visualização permitiu observar relações entre:

```text
Domínio
   ├── Domínios relacionados
   ├── DNS
   ├── Pessoas
   ├── Endereços de e-mail
   └── Servidores MX
```

O gráfico facilita a correlação das informações encontradas e demonstra uma das principais características do Maltego: representar visualmente relações entre diferentes entidades.

### 9. Encerramento

Após a conclusão da análise, o Maltego foi fechado.

Quando solicitado pelo programa, foi utilizada a opção:

```text
Discard All
```

O Terminal também foi encerrado após o término da atividade.

## Comandos utilizados

O comando utilizado para iniciar a ferramenta foi:

```bash
maltego
```

As demais etapas foram realizadas através da interface gráfica do Maltego.

## Transforms utilizados

| Transform                                     | Finalidade                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------ |
| `[Utilities] To Domains [within Properties]`  | Identificar domínios relacionados às propriedades da entidade            |
| `[Utilities] To DNSNames [within Properties]` | Obter informações relacionadas a nomes DNS                               |
| `[Utilities] To Person [PGP]`                 | Identificar possíveis pessoas relacionadas através de dados PGP públicos |
| `[Utilities] To Email Addresses [PGP]`        | Identificar endereços de e-mail presentes nas informações PGP            |
| `[Utilities] To DNS Name - MX (mail server)`  | Identificar servidores de e-mail associados ao domínio                   |

## Interpretação

A atividade demonstrou como uma única informação inicial, nesse caso o domínio `ufc.br`, pode ser utilizada como ponto de partida para uma investigação de OSINT.

A partir dos Transforms disponíveis no Maltego, foi possível expandir o conjunto de informações observadas e estabelecer relações entre:

* Domínios;
* Registros DNS;
* Pessoas;
* Endereços de e-mail;
* Servidores de e-mail;
* Informações públicas de infraestrutura.

O uso de diferentes fontes permite construir uma visão mais ampla sobre um determinado ativo sem realizar exploração ou alteração da infraestrutura analisada.

## Resultado

Foi realizada uma investigação passiva utilizando o Maltego a partir do domínio `ufc.br`.

Foram executados diferentes Transforms para expandir as informações disponíveis e visualizar relações entre o domínio, DNS, pessoas, endereços de e-mail e servidores MX.

A atividade permitiu praticar a coleta e correlação de informações públicas utilizando uma ferramenta de OSINT.

## Conceitos praticados

* OSINT
* Reconhecimento passivo
* Maltego
* Transforms
* DNS
* Registros MX
* PGP
* Endereços de e-mail
* Correlação de informações
* Reconhecimento de infraestrutura
* Inteligência de fontes abertas

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 03–04.

[Ver evidências — Aula 03–04](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-03-04/evidencias.pdf)
