# Activity 3.09 — DNS Enumeration with NSLookup

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 11–12  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use NSLookup to perform DNS queries and identify different types of records associated with a domain, including IP addresses, DNS servers, mail servers, and TXT records.

The activity demonstrates the differences between direct queries and queries performed in the tool's interactive mode, while exploring how DNS records can reveal information about a domain's infrastructure.

## Environment

- **Operating system:** Kali Linux
- **Tool:** `nslookup`
- **Domain analyzed:** `grancursosonline.com.br`
- **DNS server:** `192.168.98.2`

## Procedure

### 1. Perform an Initial Domain Query

A direct DNS query was performed using NSLookup:

```bash
sudo -i
nslookup grancursosonline.com.br
```

**Observed output:**

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

The query returned IPv4 addresses (A records) and IPv6 addresses (AAAA records) associated with the domain.

The message `Non-authoritative answer` indicates that the response was provided by the DNS resolver queried, rather than directly by an authoritative name server for the domain.

### 2. Query DNS Name Servers in Interactive Mode

NSLookup can also operate in interactive mode:

```bash
nslookup
```

Within the interactive session, the record type was set to NS:

```text
set type=ns
```

The domain was then queried:

```text
grancursosonline.com.br
```

**Observed output:**

```text
Server: 192.168.98.2
Address: 192.168.98.2#53

Non-authoritative answer:
grancursosonline.com.br nameserver = dan.ns.cloudflare.com.
grancursosonline.com.br nameserver = rita.ns.cloudflare.com.

Authoritative answers can be found from:
>
```

NS records identify the name servers associated with the domain's authoritative DNS service.

The following servers were returned:

- `dan.ns.cloudflare.com`
- `rita.ns.cloudflare.com`

This query demonstrates how NSLookup's interactive mode can be used to inspect name server records.

### 3. Query Mail Servers

While still in interactive mode, the record type was changed to MX:

```text
set type=mx
```

The domain was queried again:

```text
grancursosonline.com.br
```

**Observed output:**

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

MX (Mail Exchange) records identify the servers responsible for receiving email addressed to a domain.

The first number in each record represents the server's preference value. Lower values have higher preference.

| Preference | Mail server |
|---:|---|
| 1 | `aspmx.l.google.com` |
| 5 | `alt1.aspmx.l.google.com` |
| 5 | `alt2.aspmx.l.google.com` |
| 10 | `alt3.aspmx.l.google.com` |
| 10 | `alt4.aspmx.l.google.com` |

The results show that the queried domain published MX records associated with Google's mail infrastructure at the time of the laboratory exercise.

To exit the interactive session, the following keyboard shortcut was used:

```text
Ctrl+C
```

### 4. Query TXT Records

Finally, a direct query for TXT records was performed:

```bash
nslookup -type=txt grancursosonline.com.br
```

**Observed output:**

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

TXT records can serve several administrative and security purposes.

The observed output included the following types of information:

**Domain verification records**

Records with names such as `google-site-verification`, `atlassian-domain-verification`, `MS`, `miro-verification`, and `onetrust-domain-verification` are associated with domain verification processes for different platforms.

Their presence can indicate that domain ownership or control has been verified for particular services. However, the records alone do not establish which services are currently active or in use.

**SPF record**

The record beginning with `v=spf1` defines a Sender Policy Framework (SPF) policy used to identify mail servers authorized to send email on behalf of the domain.

The observed record references Amazon SES, Google, Zendesk, HubSpot, Salesforce, and specific IPv4 addresses. These entries indicate the sources permitted by the published SPF policy.

The `~all` mechanism indicates a soft-fail policy for sources not otherwise authorized by the SPF record. It does not, by itself, determine how every receiving mail system will handle a message.

**Multiple service integrations**

The presence of multiple verification records demonstrates how public DNS can contain information related to different service providers and administrative integrations.

#### Interpreting the TCP Retry Message

The output began with:

```text
;; Truncated, retrying in TCP mode.
```

This indicates that the DNS response received initially was truncated and that NSLookup retried the query over TCP to obtain the complete response.

DNS commonly uses UDP for queries, but TCP can be used when a response is too large to fit in the available UDP response size or when other DNS requirements call for TCP.

## Commands Used

The following commands and interactive instructions were used:

```bash
sudo -i
nslookup grancursosonline.com.br
nslookup
```

Within the interactive NSLookup session:

```text
set type=ns
grancursosonline.com.br

set type=mx
grancursosonline.com.br

Ctrl+C
```

The TXT records were then queried directly:

```bash
nslookup -type=txt grancursosonline.com.br
```

## Concepts Practiced

### NSLookup

A command-line utility used to query DNS servers and retrieve information about records associated with domain names.

### A Records

Associate a domain name with an IPv4 address.

### AAAA Records

Associate a domain name with an IPv6 address.

### NS Records

Identify name servers associated with a domain's authoritative DNS configuration.

### MX Records

Identify mail servers responsible for receiving email for a domain. The associated preference values influence the order in which mail servers are selected.

### TXT Records

Allow arbitrary text data to be published in DNS. Common uses include domain verification and email authentication policies such as SPF.

### Non-Authoritative Answer

Indicates that the response was supplied by the DNS resolver queried, rather than directly by an authoritative name server. A recursive resolver can return cached data obtained through its DNS resolution process.

### Interactive and Direct Queries

NSLookup supports both direct command-line queries and an interactive session in which the record type can be changed before querying different records.

### DNS Enumeration

DNS enumeration collects publicly available information about a domain's addressing, name servers, email infrastructure, and service integrations. This information can support reconnaissance and security assessments.

## Results

The activity demonstrated how NSLookup can be used for DNS enumeration to identify:

- IPv4 and IPv6 addresses.
- Name servers.
- Mail servers.
- TXT records.
- Services and platforms referenced in domain verification records.
- Information related to SPF email authentication policies.

The exercise reinforced the role of DNS queries in reconnaissance and infrastructure analysis without directly exploiting the services associated with the domain.

The results represent the records returned by the DNS resolver during the recorded laboratory session. DNS configurations can change, so the observed values should not be treated as a current inventory.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 11–12.

**Recorded screenshot:** Step 5 of the activity, as required by the laboratory instructions, showing the TXT record query performed with NSLookup.

[View Evidence — Classes 11–12](../evidencias.pdf)

---

[Back to Classes 11–12](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
