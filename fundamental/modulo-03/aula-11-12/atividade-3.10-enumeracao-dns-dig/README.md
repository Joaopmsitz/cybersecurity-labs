# Atividade 3.10 — Enumeração DNS com DIG

## Objetivo

Utilizar o **DIG (Domain Information Groper)** para realizar consultas DNS e analisar diferentes tipos de registros de um domínio.

A atividade explora consultas dos registros **A, NS, MX, AAAA e CNAME**, permitindo observar informações de resolução, servidores DNS, infraestrutura de e-mail, endereços IPv6 e a resposta retornada quando não existe um registro CNAME para o domínio consultado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** `dig`
* **Domínio analisado:** `grancursosonline.com.br`
* **Servidor DNS utilizado:** `192.168.98.2`

---

## 1. Consulta da ajuda do DIG

Primeiramente, foi verificada a ajuda da ferramenta:

```bash
sudo -i
dig -h
```

A execução apresenta as opções disponíveis para realização das consultas DNS, incluindo especificação de tipos de registros, servidores DNS, opções de consulta e parâmetros de saída.

---

## 2. Consulta do registro A

Foi realizada uma consulta padrão para o domínio:

```bash
dig grancursosonline.com.br
```

Saída:

```text
; <<>> DiG 9. 20.11-4+b1-Debian <<>> grancursosonline.com.br
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47611
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	A

;; ANSWER SECTION:
grancursosonline.com.br. 300	IN	A	104.18.100.225
grancursosonline.com.br. 300	IN	A	104.18.99.225

;; Query time: 4 msec
;; SERVER: 192.168.98.2#53(192.168.98.2) (UDP)
;; WHEN: Fri Feb 09 16:16:08 -03 2024
;; MSG SIZE  rcvd: 84
```

O registro consultado foi o **A**, responsável por associar o domínio a endereços IPv4.

Nesse resultado foram encontrados dois endereços:

* `104.18.100.225`
* `104.18.99.225`

### Estrutura da resposta

O `DIG` apresenta várias informações úteis além do resultado final:

* `status: NOERROR` — a consulta foi processada sem erro DNS.
* `QUERY: 1` — uma pergunta foi realizada.
* `ANSWER: 2` — dois registros foram retornados na seção de resposta.
* `AUTHORITY: 0` — nenhum registro foi retornado na seção de autoridade.
* `SERVER: 192.168.98.2#53` — servidor DNS utilizado.
* `Query time: 4 msec` — tempo de resposta observado.
* `TTL 300` — tempo, em segundos, pelo qual a resposta pode permanecer em cache.

---

## 3. Consulta dos servidores DNS

Foi realizada uma consulta específica pelo registro `NS`:

```bash
dig grancursosonline.com.br -t ns
```

O resultado apresentou os servidores:

```text
grancursosonline.com.br. 300	IN	NS	rita.ns.cloudflare.com.
grancursosonline.com.br. 300	IN	NS	dan.ns.cloudflare.com.
```

Os registros **NS (Name Server)** identificam os servidores DNS responsáveis pelo domínio.

Nesse resultado, os servidores encontrados foram:

* `rita.ns.cloudflare.com.`
* `dan.ns.cloudflare.com.`

---

## 4. Consulta dos servidores de e-mail

Em seguida, foi realizada uma consulta aos registros `MX`:

```bash
dig grancursosonline.com.br -t mx
```

O resultado apresentou:

```text
grancursosonline.com.br. 300	IN	MX	1 aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt1.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt2.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt3.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt4.aspmx.l.google.com.
```

Os registros **MX (Mail Exchange)** indicam os servidores responsáveis pelo recebimento de e-mails do domínio.

A prioridade é determinada pelo número associado ao registro. Quanto **menor o valor**, maior a prioridade.

| Prioridade | Servidor                   |
| ---------: | -------------------------- |
|          1 | `aspmx.l.google.com.`      |
|          5 | `alt1.aspmx.l.google.com.` |
|          5 | `alt2.aspmx.l.google.com.` |
|         10 | `alt3.aspmx.l.google.com.` |
|         10 | `alt4.aspmx.l.google.com.` |

O resultado indica a utilização de infraestrutura de e-mail do Google para o domínio analisado.

---

## 5. Consulta do registro AAAA

Também foi realizada uma consulta específica para registros `AAAA`:

```bash
dig grancursosonline.com.br AAAA
```

Resultado observado:

```text
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:64e1
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:63e1
```

O registro **AAAA** é utilizado para endereços IPv6.

Nesse caso, foram identificados dois endereços IPv6 associados ao domínio:

* `2606:4700::6812:64e1`
* `2606:4700::6812:63e1`

---

## 6. Consulta do registro CNAME

Por fim, foi realizada a consulta solicitada pelo roteiro para verificar a existência de um registro `CNAME`:

```bash
dig grancursosonline.com.br CNAME
```

Saída:

```text
; <<>> DiG 9.20.11-4+b1-Debian <<>> grancursosonline.com.br CNAME
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5445
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;grancursosonline.com.br.	IN	CNAME

;; AUTHORITY SECTION:
grancursosonline.com.br. 300	IN	SOA	dan.ns.cloudflare.com. dns.cloudflare.com. 2332988706 10000 2400 604800 1800

;; Query time: 8 msec
;; SERVER: 192.168.98.2#53(192.168.98.2) (UDP)
;; WHEN: Fri Feb 09 16:35:34 -03 2024
;; MSG SIZE  rcvd: 113
```

Nesse resultado, o campo:

```text
ANSWER: 0
```

indica que nenhum registro `CNAME` foi retornado para o nome consultado.

A resposta também apresenta uma seção `AUTHORITY` contendo um registro **SOA (Start of Authority)**:

```text
grancursosonline.com.br. 300 IN SOA dan.ns.cloudflare.com. dns.cloudflare.com. 2332988706 10000 2400 604800 1800
```

O registro SOA contém informações administrativas e de controle da zona DNS, incluindo o servidor de nomes principal, o responsável pela zona em formato DNS e parâmetros relacionados à atualização e ao cache.

A presença do SOA na resposta, juntamente com `ANSWER: 0`, faz parte da resposta DNS utilizada para indicar que não houve um registro CNAME retornado para o nome consultado.

---

## Conceitos praticados

### DIG

O `dig` é uma ferramenta de consulta DNS que permite analisar detalhadamente as respostas recebidas de um servidor DNS.

### A

Registro utilizado para associar um domínio a um endereço IPv4.

### AAAA

Registro utilizado para associar um domínio a um endereço IPv6.

### NS

Identifica os servidores DNS responsáveis pela zona do domínio.

### MX

Identifica os servidores responsáveis pelo recebimento de e-mails do domínio e suas respectivas prioridades.

### CNAME

Registro utilizado para criar um alias DNS que aponta para outro nome de domínio.

### SOA

O registro **Start of Authority** contém informações administrativas da zona DNS, incluindo o servidor autoritativo principal e parâmetros de controle da zona.

### TTL

**Time To Live** determina por quanto tempo uma resposta DNS pode permanecer armazenada em cache antes de precisar ser consultada novamente.

### ANSWER / AUTHORITY

O `DIG` divide a resposta DNS em diferentes seções. `ANSWER` contém os registros que respondem diretamente à consulta, enquanto `AUTHORITY` pode conter informações relacionadas à autoridade da zona envolvida na resposta.

---

## Resultado

A atividade demonstrou o uso do `dig` para realizar **enumeração e análise de registros DNS**, permitindo identificar:

* Endereços IPv4;
* Endereços IPv6;
* Servidores DNS;
* Servidores de e-mail;
* Prioridades dos registros MX;
* Informações de autoridade da zona;
* Ausência de um registro CNAME na resposta analisada;
* Informações de TTL, servidor DNS e tempo de resposta.

Em comparação com uma consulta DNS simples, o `dig` fornece uma saída mais detalhada, permitindo analisar não apenas o registro retornado, mas também os metadados da resposta DNS.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 11 e 12**](../evidencias.pdf)

**Print registrado:** etapa 7 da atividade, conforme solicitado pelo roteiro, mostrando a consulta do registro CNAME com `dig`.
