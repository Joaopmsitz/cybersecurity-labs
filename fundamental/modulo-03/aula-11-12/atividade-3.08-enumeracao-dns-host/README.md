# Atividade 3.8 — Enumeração DNS com `host` no Kali Linux

## Objetivo

Utilizar a ferramenta `host` no Kali Linux para realizar consultas DNS e identificar diferentes tipos de registros associados a domínios, incluindo endereços IPv4, IPv6, servidores de nomes (NS) e servidores de e-mail (MX).

A atividade foi realizada em ambiente de laboratório e os procedimentos foram utilizados exclusivamente para fins acadêmicos.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** `host`
* **Interface de rede:** `eth0`
* **IP do laboratório:** `192.168.98.40`

---

## 1. Acesso como superusuário

No Terminal, foi executado:

```bash
sudo -i
```

A autenticação foi realizada utilizando a senha fornecida pelo ambiente de laboratório.

Após a autenticação, o terminal passou a operar como `root`.

---

## 2. Consulta dos registros DNS de um domínio

Para consultar os registros DNS de `grancursos.com.br`, foi utilizado:

```bash
host grancursos.com.br
```

Saída observada:

```text
grancursos.com.br has address 172.67.175.92
grancursos.com.br has address 104.21.35.137
grancursos.com.br has IPv6 address 2606:4700:3034::6815:2389
grancursos.com.br has IPv6 address 2606:4700:3037::ac43:af5c
grancursos.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursos.com.br mail is handled by 1 aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursos.com.br mail is handled by 5 alt1.aspmx.l.google.com.
grancursos.com.br has HTTP service bindings 1 . alpn="h3,h2" ipv4hint=104.21.35.137,172.67.175.92 ech=AEX+DQBB7AAgACD6/cO4qr6UO3EzTMimuo76z5YLNjJw83UKXcPBkZwMLgAEAAEAAQASY2xvdWRmbGFyZS1lY2guY29tAAA= ipv6hint=2606:4700:3034::6815:2389,2606:4700:3037::ac43:af5c
```

A saída permite observar diferentes informações DNS de uma única consulta.

### Registros A

```text
grancursos.com.br has address 172.67.175.92
grancursos.com.br has address 104.21.35.137
```

São endereços IPv4 associados ao domínio, correspondentes a registros `A`.

A existência de mais de um endereço IPv4 permite que um domínio tenha múltiplos pontos de atendimento ou infraestrutura distribuída.

### Registros AAAA

```text
grancursos.com.br has IPv6 address 2606:4700:3034::6815:2389
grancursos.com.br has IPv6 address 2606:4700:3037::ac43:af5c
```

São endereços IPv6 associados ao domínio, correspondentes a registros `AAAA`.

### Registros MX

Também foram identificados servidores responsáveis pelo recebimento de e-mails:

```text
grancursos.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursos.com.br mail is handled by 1 aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursos.com.br mail is handled by 5 alt1.aspmx.l.google.com.
```

O número antes do servidor representa a **preferência** do registro MX. Números menores possuem maior prioridade de entrega.

Nesse resultado, `aspmx.l.google.com` possui preferência `1`, enquanto `alt1` e `alt2` possuem preferência `5`, e `alt3` e `alt4`, preferência `10`.

### Registro HTTPS/SVCB

Também apareceu um registro de associação de serviço HTTP:

```text
grancursos.com.br has HTTP service bindings 1 . alpn="h3,h2" ...
```

O campo `alpn="h3,h2"` indica suporte anunciado para HTTP/3 e HTTP/2.

Os campos `ipv4hint` e `ipv6hint` fornecem endereços que podem ser utilizados como informações auxiliares para conexão.

---

## 3. Consulta dos servidores de nomes

Foi realizada uma consulta específica pelo tipo `NS`:

```bash
host -t ns esr.rnp.br
```

Resultado:

```text
esr.rnp.br has no NS record
```

A opção:

```text
-t ns
```

define que a consulta deve procurar registros **NS (Name Server)**.

O resultado apresentado pelo ambiente indica que não foi retornado um registro NS para `esr.rnp.br` nessa consulta.

Esse resultado deve ser interpretado como a resposta obtida pelo resolvedor utilizado no laboratório, sem concluir, isoladamente, que o domínio não possui infraestrutura DNS autoritativa.

---

## 4. Consulta dos Name Servers de outro domínio

Foi realizada uma nova consulta utilizando:

```bash
host -t ns grancursosonline.com.br
```

Saída observada:

```text
grancursosonline.com.br name server rachel.ns.cloudflare.com.
grancursosonline.com.br name server josh.ns.cloudflare.com.
```

O registro `NS` informa quais servidores de nomes estão associados ao domínio.

Nesse caso, foram retornados:

```text
rachel.ns.cloudflare.com.
josh.ns.cloudflare.com.
```

A consulta demonstra como o `host` pode ser utilizado para identificar os servidores de nomes publicados para um domínio.

---

## 5. Enumeração dos servidores de e-mail

A etapa final utilizou uma consulta específica para registros `MX`:

```bash
host -t mx grancursosonline.com.br
```

Saída observada:

```text
grancursosonline.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt1.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 1 aspmx.l.google.com.
```

Os registros encontrados foram:

| Preferência | Servidor MX               |
| ----------: | ------------------------- |
|           1 | `aspmx.l.google.com`      |
|           5 | `alt1.aspmx.l.google.com` |
|           5 | `alt2.aspmx.l.google.com` |
|          10 | `alt3.aspmx.l.google.com` |
|          10 | `alt4.aspmx.l.google.com` |

A preferência determina a ordem utilizada pelos sistemas de entrega de e-mail: **quanto menor o valor, maior a preferência**.

Nesse resultado, `aspmx.l.google.com` possui a menor preferência numérica (`1`), seguido pelos servidores com preferência `5` e, posteriormente, pelos servidores com preferência `10`.

Essa consulta demonstra como informações sobre a infraestrutura de e-mail podem ser obtidas por meio de registros DNS publicados pelo próprio domínio.

---

## Conceitos praticados

### DNS

O **Domain Name System (DNS)** é utilizado para associar nomes de domínio a diferentes tipos de informações, como endereços IP, servidores de nomes e servidores de e-mail.

### `host`

O `host` é uma ferramenta de linha de comando utilizada para realizar consultas DNS de forma simples.

Exemplos utilizados na atividade:

```bash
host dominio
host -t ns dominio
host -t mx dominio
```

### Registro A

Relaciona um nome de domínio a um endereço **IPv4**.

### Registro AAAA

Relaciona um nome de domínio a um endereço **IPv6**.

### Registro NS

Identifica servidores de nomes associados ao domínio.

### Registro MX

Identifica os servidores responsáveis pelo recebimento de e-mails de um domínio e suas respectivas preferências.

---

## Resultado

A atividade permitiu utilizar o `host` para consultar diferentes informações publicadas no DNS de domínios.

Foram realizadas consultas para:

* registros IPv4 (`A`);
* registros IPv6 (`AAAA`);
* servidores de nomes (`NS`);
* servidores de e-mail (`MX`);
* informações adicionais relacionadas ao serviço HTTP.

A prática demonstra como consultas DNS podem ser utilizadas em uma etapa de **enumeração e reconhecimento passivo**, permitindo compreender a infraestrutura publicada por um domínio sem realizar exploração do serviço.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 11 e 12**](../evidencias.pdf)

**Print registrado:** etapa 5 da atividade, conforme solicitado pelo roteiro, mostrando a consulta dos registros MX com `host`.
