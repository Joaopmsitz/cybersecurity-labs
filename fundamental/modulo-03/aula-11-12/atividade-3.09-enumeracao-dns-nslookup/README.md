# Atividade 3.9 — Enumeração DNS com NSLookup

## Objetivo

Utilizar o **NSLookup** para realizar consultas DNS e identificar diferentes tipos de registros de um domínio, incluindo endereços IP, servidores DNS, servidores de e-mail e registros TXT.

A atividade permite observar a diferença entre consultas diretas e consultas realizadas no modo interativo da ferramenta, além de compreender como os registros DNS podem fornecer informações sobre a infraestrutura de um domínio.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** `nslookup`
* **Domínio analisado:** `grancursosonline.com.br`
* **Servidor DNS utilizado:** `192.168.98.2`

---

## 1. Consulta inicial do domínio

Primeiramente, foi realizada uma consulta direta utilizando o `nslookup`:

```bash
sudo -i
nslookup grancursosonline.com.br
```

Saída observada:

```text
Server: 192.168.98.2
Address: 192.168.98.2#53

Non-authoritative answer:
Name:   grancursosonline.com.br
Address: 104.18.99.225
Name:   grancursosonline.com.br
Address: 104.18.100.225
Name:   grancursosonline.com.br
Address: 2606:4700::6812:63e1
Name:   grancursosonline.com.br
Address: 2606:4700::6812:64e1
```

A consulta retornou endereços **IPv4 (A)** e **IPv6 (AAAA)** associados ao domínio.

A indicação `Non-authoritative answer` significa que a resposta foi fornecida pelo servidor DNS consultado, e não diretamente por um servidor autoritativo do domínio.

---

## 2. Consulta interativa de servidores DNS

O `nslookup` também pode ser utilizado em modo interativo:

```bash
nslookup
```

Dentro do modo interativo, foi definido o tipo de registro como `NS`:

```text
set type=ns
```

Em seguida, foi consultado o domínio:

```text
grancursosonline.com.br
```

Saída:

```text
Server: 192.168.98.2
Address: 192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br nameserver = dan.ns.cloudflare.com.
grancursosonline.com.br nameserver = rita.ns.cloudflare.com.

Authoritative answers can be found from:
>
```

Os registros **NS (Name Server)** identificam os servidores responsáveis pelo serviço DNS autoritativo do domínio.

Nesse resultado, foram identificados:

* `dan.ns.cloudflare.com`
* `rita.ns.cloudflare.com`

---

## 3. Consulta dos servidores de e-mail

Ainda no modo interativo, foi alterado o tipo de consulta para `MX`:

```text
set type=mx
```

Depois:

```text
grancursosonline.com.br
```

Saída:

```text
Server: 192.168.98.2
Address: 192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br mail exchanger = 1 aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 10 alt3.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 10 alt4.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 5 alt1.aspmx.l.google.com.
grancursosonline.com.br mail exchanger = 5 alt2.aspmx.l.google.com.
```

Os registros **MX (Mail Exchange)** indicam quais servidores recebem e-mails destinados ao domínio.

A preferência é representada pelo primeiro número de cada registro. Valores menores possuem maior prioridade.

| Prioridade | Servidor                  |
| ---------: | ------------------------- |
|          1 | `aspmx.l.google.com`      |
|          5 | `alt1.aspmx.l.google.com` |
|          5 | `alt2.aspmx.l.google.com` |
|         10 | `alt3.aspmx.l.google.com` |
|         10 | `alt4.aspmx.l.google.com` |

Os resultados mostram a utilização de infraestrutura de e-mail do Google para o domínio consultado.

Para sair do modo interativo:

```text
Ctrl+C
```

---

## 4. Consulta de registros TXT

Por fim, foi realizada uma consulta direta aos registros **TXT**:

```bash
nslookup -type=txt grancursosonline.com.br
```

Saída observada:

```text
;; Truncated, retrying in TCP mode.
Server: 192.168.98.2
Address: 192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br text = "google-site-verification=bJj3VTcb9ZUQDOPT5SbS_5nkfsr-Raw9oh8ptw01MRM"
grancursosonline.com.br text = "google-site-verification=xiBkOcAELpzCJlFjzARMpyCQpajShwRZ0RwuDQY3V2U"
grancursosonline.com.br text = "atlassian-domain-verification=8xiJYcQ1gnysutOmpxf6x8cvLNZyaARmLpR2YqL3Dz6Stz0PwHXZczMQxR6vF9Vx"
grancursosonline.com.br text = "v=spf1 include:amazonses.com include:_spf.google.com include:mail.zendesk.com include:302036.spf06.hubspotemail.net include:_spf.salesforce.com ip4:168.245.107.217 ip4:168.245.71.19 ~all"
grancursosonline.com.br text = "MS=ms15123477"
grancursosonline.com.br text = "Validity-DomainVerification=Dnd+gzxPqOUWqJwGPCbe9a62tic="
grancursosonline.com.br text = "miro-verification=4394c3b7962ee08e2046f11b82c381e37dc66d49"
grancursosonline.com.br text = "onetrust-domain-verification=caf3e6b8fb9c49bebabf05dfb1697e9b"
grancursosonline.com.br text = "google-site-verification=1m2tQHRTA5e4GsKQNx_tKHKsw_vEVEKmYvfZyFqdA1o"
grancursosonline.com.br text = "google-site-verification=4pYdXVBpN4LSXBeZO9rx3B4rnwOpKaNx3oL-Ue2Ntro"
grancursosonline.com.br text = "google-site-verification=BH-6GXNCScJusTX7ROYHrxvvYH9c21yIbx5UHvdOgvQ"
grancursosonline.com.br text = "google-site-verification=JoSCARaYBckFvemdRfu8wT2N5GX4EO43Hg80c43UBI0"
grancursosonline.com.br text = "google-site-verification=atopuSr7BiVqBseFzJr4OII1FZtMEoSeA09MYZE7sRo"
```

Os registros TXT podem ser utilizados para diferentes finalidades administrativas e de segurança.

No resultado, é possível identificar:

* **Verificações de domínio:** registros utilizados por serviços como Google, Atlassian, Microsoft, Miro e OneTrust.
* **SPF:** o registro iniciado por `v=spf1` define uma política para identificar servidores autorizados a enviar e-mails em nome do domínio.
* **Múltiplos serviços:** a existência de vários registros de verificação demonstra a integração do domínio com diferentes plataformas.

A mensagem:

```text
;; Truncated, retrying in TCP mode.
```

indica que a resposta DNS inicialmente excedeu o limite de uma consulta UDP e o `nslookup` repetiu a consulta utilizando TCP para obter a resposta completa.

---

## Conceitos praticados

### NSLookup

Ferramenta utilizada para consultar servidores DNS e obter informações sobre registros associados a domínios.

### A

Registro que associa um domínio a um endereço **IPv4**.

### AAAA

Registro utilizado para associar um domínio a um endereço **IPv6**.

### NS

Identifica os servidores DNS autoritativos responsáveis pelo domínio.

### MX

Identifica os servidores responsáveis pelo recebimento de e-mails do domínio. O número associado ao registro representa sua prioridade.

### TXT

Permite armazenar informações textuais no DNS. É utilizado, entre outras finalidades, para verificações de domínio e políticas de autenticação de e-mail, como SPF.

### Non-authoritative answer

Indica que a resposta foi obtida através do servidor DNS consultado, em vez de ser retornada diretamente por um servidor autoritativo.

---

## Resultado

A atividade demonstrou como o `nslookup` pode ser utilizado para realizar **enumeração DNS passiva**, permitindo identificar:

* Endereços IPv4 e IPv6;
* Servidores DNS;
* Servidores de e-mail;
* Registros TXT;
* Serviços e plataformas associados ao domínio;
* Informações relacionadas à política SPF.

A consulta de registros DNS é uma etapa importante de reconhecimento, pois permite compreender parte da infraestrutura pública associada a um domínio sem realizar exploração do alvo.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 11 e 12**](../evidencias.pdf)

**Print registrado:** etapa 5 da atividade, conforme solicitado pelo roteiro, mostrando a consulta dos registros TXT com `nslookup`.
