# Atividade 1.7 — Explorando a ferramenta WHOIS no Kali Linux

## Objetivo

Utilizar a ferramenta `whois` para consultar informações públicas relacionadas ao registro de domínios e observar dados como entidade responsável, contatos técnicos e servidores DNS.

Foram realizadas consultas em três domínios para comparar as informações disponibilizadas pelo serviço de registro.

## Ambiente

* Kali Linux
* Terminal
* WHOIS
* Registro.br

## Procedimento

### 1. Acesso ao modo administrador

Foi aberto o Terminal e utilizado o `sudo` para acessar o modo administrador:

```bash
sudo -i
```

### 2. Consulta do domínio `esr.rnp.br`

A primeira consulta foi realizada utilizando:

```bash
whois esr.rnp.br
```

A resposta apresentou informações relacionadas ao domínio `rnp.br`, incluindo:

* Entidade responsável pelo domínio;
* Identificadores de proprietário e contato técnico;
* Servidores de nomes (DNS);
* Endereços IPv4 e IPv6 associados aos servidores;
* Data de criação e alteração do registro;
* Status do domínio.

Entre os campos observados estavam:

```text
domain
owner
owner-c
tech-c
nserver
created
changed
status
```

O campo `nserver` permite identificar os servidores DNS responsáveis pela resolução do domínio.

### 3. Consulta do domínio `guanambi.ba.gov.br`

Em seguida, foi realizada uma consulta para um domínio governamental:

```bash
whois guanambi.ba.gov.br
```

A consulta retornou informações referentes ao domínio `ba.gov.br`, incluindo a entidade responsável pelo registro e os servidores DNS utilizados.

Também foram observados campos como:

```text
domain
owner
owner-c
tech-c
nserver
created
changed
status
```

A consulta permitiu identificar a estrutura de registro utilizada para um domínio governamental e os servidores responsáveis pela resolução DNS.

### 4. Consulta do domínio `itapaje.ce.gov.br`

Por fim, foi realizada uma terceira consulta:

```bash
whois itapaje.ce.gov.br
```

O resultado apresentou informações referentes ao domínio `ce.gov.br`, incluindo:

* Entidade responsável pelo domínio;
* Identificador do proprietário;
* Identificador do contato técnico;
* Servidores DNS;
* Endereços IPv4 e IPv6;
* Datas relacionadas ao registro;
* Status do domínio.

Essa foi a consulta utilizada como evidência principal da atividade.

## Comandos utilizados

```bash
sudo -i

whois esr.rnp.br

whois guanambi.ba.gov.br

whois itapaje.ce.gov.br
```

## Interpretação

O WHOIS permite consultar informações públicas associadas ao registro de determinados domínios.

Durante a atividade, alguns dos principais campos analisados foram:

| Campo     | Significado                           |
| --------- | ------------------------------------- |
| `domain`  | Domínio ou zona consultada            |
| `owner`   | Entidade associada ao registro        |
| `owner-c` | Identificador do contato/proprietário |
| `tech-c`  | Identificador do contato técnico      |
| `nserver` | Servidores DNS associados             |
| `created` | Data de criação do registro           |
| `changed` | Data da última alteração registrada   |
| `status`  | Estado do registro do domínio         |

As informações obtidas podem ser utilizadas em atividades de reconhecimento e OSINT, pois ajudam a entender a infraestrutura pública associada a um domínio.

## Resultado

Foram realizadas consultas WHOIS em três domínios e analisadas informações públicas relacionadas aos seus registros.

A atividade permitiu observar principalmente:

* Dados de registro de domínios;
* Entidades associadas aos registros;
* Contatos identificados por handles;
* Servidores DNS;
* Endereços IP associados aos servidores;
* Datas e status dos registros.

## Conceitos praticados

* WHOIS
* OSINT
* Reconhecimento passivo
* Registro de domínios
* DNS
* Nameservers
* Informações públicas de infraestrutura
* Reconhecimento de ativos

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 03–04.

[Ver evidências — Aula 03–04](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-03-04/evidencias.pdf)
