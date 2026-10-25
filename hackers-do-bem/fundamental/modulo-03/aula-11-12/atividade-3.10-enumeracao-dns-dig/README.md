# Activity 3.10 — DNS Enumeration with DIG

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 11–12  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use DIG (Domain Information Groper) to perform DNS queries and analyze different types of records associated with a domain.

The activity covers queries for A, NS, MX, AAAA, and CNAME records, allowing the observation of DNS resolution information, name servers, email infrastructure, IPv6 addresses, and the response returned when no CNAME record is provided for the queried domain name.

## Environment

- **Operating system:** Kali Linux
- **Tool:** `dig`
- **Domain analyzed:** `grancursosonline.com.br`
- **DNS server:** `192.168.98.2`

## Procedure

### 1. Display DIG Help

First, the tool's help information was requested:

```bash
sudo -i
dig -h
```

The help output provides the available options for performing DNS queries, including record type selection, DNS server specification, query options, and output parameters.

### 2. Query the A Record

A standard DNS query was performed for the domain:

```bash
dig grancursosonline.com.br
```

**Observed output:**

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

The queried record type was **A**, which associates a domain name with IPv4 addresses.

Two addresses were returned:

- `104.18.100.225`
- `104.18.99.225`

#### Understanding the Response Structure

DIG provides useful information beyond the returned records:

- `status: NOERROR` — the DNS query completed without a DNS error.
- `QUERY: 1` — one question was included in the query.
- `ANSWER: 2` — two records were returned in the answer section.
- `AUTHORITY: 0` — no records were returned in the authority section.
- `SERVER: 192.168.98.2#53` — the DNS server used for the query.
- `Query time: 4 msec` — the observed response time.
- `TTL 300` — the response's time-to-live value, in seconds, which affects how long it can remain cached.

The `NOERROR` status indicates that the DNS query completed successfully; it does not, by itself, guarantee that every requested record type exists.

### 3. Query Name Servers

A query specifically targeting NS records was performed:

```bash
dig grancursosonline.com.br -t ns
```

The following name servers were returned:

```text
grancursosonline.com.br. 300	IN	NS	rita.ns.cloudflare.com.
grancursosonline.com.br. 300	IN	NS	dan.ns.cloudflare.com.
```

NS (Name Server) records identify the name servers associated with a domain's DNS delegation.

The servers returned in this laboratory query were:

- `rita.ns.cloudflare.com.`
- `dan.ns.cloudflare.com.`

These results reflect the DNS configuration observed during the recorded exercise.

### 4. Query Mail Servers

Next, an MX record query was performed:

```bash
dig grancursosonline.com.br -t mx
```

The following output was observed:

```text
grancursosonline.com.br. 300	IN	MX	1 aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt1.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	5 alt2.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt3.aspmx.l.google.com.
grancursosonline.com.br. 300	IN	MX	10 alt4.aspmx.l.google.com.
```

MX (Mail Exchange) records identify the mail servers responsible for receiving email for a domain.

The preference value is the number associated with each record. Lower values indicate higher preference.

| Preference | Mail server |
|---:|---|
| 1 | `aspmx.l.google.com.` |
| 5 | `alt1.aspmx.l.google.com.` |
| 5 | `alt2.aspmx.l.google.com.` |
| 10 | `alt3.aspmx.l.google.com.` |
| 10 | `alt4.aspmx.l.google.com.` |

The results indicate that the domain's observed email configuration used Google's mail infrastructure.

### 5. Query the AAAA Record

A query specifically targeting AAAA records was also performed:

```bash
dig grancursosonline.com.br AAAA
```

**Observed output:**

```text
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:64e1
grancursosonline.com.br. 300	IN	AAAA	2606:4700::6812:63e1
```

AAAA records associate a domain name with IPv6 addresses.

Two IPv6 addresses were identified:

- `2606:4700::6812:64e1`
- `2606:4700::6812:63e1`

These records demonstrate how a domain can publish IPv6 addresses alongside its IPv4 addressing information.

### 6. Query the CNAME Record

Finally, a query was performed to check for a CNAME record:

```bash
dig grancursosonline.com.br CNAME
```

**Observed output:**

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

In this response, the field:

```text
ANSWER: 0
```

indicates that no CNAME record was returned for the queried name.

The response also includes an authority section containing an SOA (Start of Authority) record:

```text
grancursosonline.com.br. 300 IN SOA dan.ns.cloudflare.com. dns.cloudflare.com. 2332988706 10000 2400 604800 1800
```

The SOA record contains administrative information about the DNS zone, including the primary name server, the responsible party's DNS-format identifier, and parameters related to zone refresh and caching.

The SOA record, together with `ANSWER: 0`, forms part of the DNS response indicating that no CNAME record was returned for the queried name.

**Technical note:** The absence of a CNAME answer does not necessarily indicate a DNS error. A name that has other record types, such as A, NS, or MX records, generally cannot also be configured as a CNAME at the same owner name. The response is consistent with the domain being queried directly for a record type it does not return.

## Commands Used

The following commands were used throughout the activity:

```bash
sudo -i
dig -h
dig grancursosonline.com.br
dig grancursosonline.com.br -t ns
dig grancursosonline.com.br -t mx
dig grancursosonline.com.br AAAA
dig grancursosonline.com.br CNAME
```

## Concepts Practiced

### DIG

DIG (Domain Information Groper) is a DNS query utility that provides detailed information about responses received from a DNS server.

### A Record

Associates a domain name with an IPv4 address.

### AAAA Record

Associates a domain name with an IPv6 address.

### NS Record

Identifies name servers associated with a domain's DNS zone.

### MX Record

Identifies the mail servers responsible for receiving email for a domain and their respective preference values.

### CNAME Record

Creates a DNS alias that points to another domain name. A CNAME record cannot normally coexist with other record types at the same DNS name.

### SOA Record

The Start of Authority record contains administrative information about a DNS zone, including its primary name server and zone-control parameters.

### TTL

Time to Live specifies how long a DNS response may remain in a cache before it needs to be refreshed.

### ANSWER and AUTHORITY Sections

DIG divides DNS responses into multiple sections:

- **ANSWER** contains records that directly answer the query.
- **AUTHORITY** can contain information about the authority for the relevant DNS zone, including SOA records in certain responses.

### DNS Enumeration

DNS enumeration involves querying DNS records to gather information about a domain's addressing, name servers, email infrastructure, and other published configuration details.

## Results

The activity demonstrated how DIG can be used for DNS enumeration and record analysis, allowing the identification of:

- IPv4 addresses.
- IPv6 addresses.
- Name servers.
- Mail servers.
- MX preference values.
- Zone authority information.
- The absence of a CNAME answer in the recorded query.
- TTL values, the DNS resolver used, and response times.

Compared with a basic DNS lookup, DIG provides a more detailed output that allows analysts to inspect not only the returned records but also the metadata associated with the DNS response.

The results documented here represent the records returned during the laboratory session in February 2024 and should not be treated as a current DNS inventory.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 11–12.

**Recorded screenshot:** Step 7 of the activity, as required by the laboratory instructions, showing the CNAME query performed with DIG.

[View Evidence — Classes 11–12](../evidencias.pdf)

---

[Back to Classes 11–12](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
