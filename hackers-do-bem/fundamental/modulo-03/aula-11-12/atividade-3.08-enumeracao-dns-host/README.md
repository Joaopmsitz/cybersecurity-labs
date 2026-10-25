# Activity 3.08 — DNS Enumeration with `host` on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 11–12  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use the `host` utility on Kali Linux to perform DNS queries and identify different types of records associated with domain names, including IPv4 addresses, IPv6 addresses, name servers (NS), and mail servers (MX).

The activity was performed in a laboratory environment for academic purposes.

## Environment

- **Operating system:** Kali Linux
- **Tool:** `host`
- **Network interface:** `eth0`
- **Laboratory IP address:** `192.168.98.40`

## Procedure

### 1. Obtain Superuser Access

The following command was executed in the terminal:

```bash
sudo -i
```

Authentication was completed using the password provided by the laboratory environment.

After authentication, the terminal operated as the `root` user.

### 2. Query DNS Records for a Domain

The following command was used to query DNS records for `grancursos.com.br`:

```bash
host grancursos.com.br
```

**Observed output:**

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

The output shows several types of DNS information returned by a single query.

#### A Records

```text
grancursos.com.br has address 172.67.175.92
grancursos.com.br has address 104.21.35.137
```

These are IPv4 addresses associated with the domain, corresponding to **A records**.

A domain can have multiple IPv4 addresses to support distributed infrastructure, traffic management, or multiple service endpoints.

#### AAAA Records

```text
grancursos.com.br has IPv6 address 2606:4700:3034::6815:2389
grancursos.com.br has IPv6 address 2606:4700:3037::ac43:af5c
```

These are IPv6 addresses associated with the domain, corresponding to **AAAA records**.

#### MX Records

The query also identified mail servers responsible for receiving email:

```text
grancursos.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursos.com.br mail is handled by 1 aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursos.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursos.com.br mail is handled by 5 alt1.aspmx.l.google.com.
```

The number preceding each server represents the **MX preference value**. Lower values indicate higher preference when selecting a mail server.

In this result, `aspmx.l.google.com` has preference `1`, while `alt1` and `alt2` have preference `5`, and `alt3` and `alt4` have preference `10`.

#### HTTPS/SVCB Service Binding Record

The output also included an HTTP service binding record:

```text
grancursos.com.br has HTTP service bindings 1 . alpn="h3,h2" ipv4hint=104.21.35.137,172.67.175.92 ech=AEX+DQBB7AAgACD6/cO4qr6UO3EzTMimuo76z5YLNjJw83UKXcPBkZwMLgAEAAEAAQASY2xvdWRmbGFyZS1lY2guY29tAAA= ipv6hint=2606:4700:3034::6815:2389,2606:4700:3037::ac43:af5c
```

This is service-binding information associated with HTTP, represented by the HTTPS/SVCB DNS record mechanism.

The field `alpn="h3,h2"` advertises support for HTTP/3 and HTTP/2 application protocols.

The `ipv4hint` and `ipv6hint` fields provide IP address hints that can assist clients when establishing connections. These hints are supplementary information rather than a replacement for ordinary address records.

### 3. Query Name Server Records

A query specifically targeting NS records was performed:

```bash
host -t ns esr.rnp.br
```

**Observed result:**

```text
esr.rnp.br has no NS record
```

The option:

```text
-t ns
```

specifies that the query should request **NS (Name Server)** records.

The result indicates that the resolver used in the laboratory did not return an NS record for `esr.rnp.br` in this query.

This result must be interpreted in the context of the specific DNS response. It does not, by itself, establish that the domain lacks authoritative DNS infrastructure.

### 4. Query Name Servers for Another Domain

A new query was performed:

```bash
host -t ns grancursosonline.com.br
```

**Observed output:**

```text
grancursosonline.com.br name server rachel.ns.cloudflare.com.
grancursosonline.com.br name server josh.ns.cloudflare.com.
```

An NS record identifies name servers associated with a domain.

The following names were returned:

```text
rachel.ns.cloudflare.com.
josh.ns.cloudflare.com.
```

This query demonstrates how `host` can be used to identify name servers published for a domain.

The output records the result observed during the laboratory exercise and should not be assumed to represent the domain's current DNS configuration.

### 5. Enumerate Mail Servers

The final query specifically targeted MX records:

```bash
host -t mx grancursosonline.com.br
```

**Observed output:**

```text
grancursosonline.com.br mail is handled by 10 alt3.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 10 alt4.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt1.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 5 alt2.aspmx.l.google.com.
grancursosonline.com.br mail is handled by 1 aspmx.l.google.com.
```

The following MX records were identified:

| Preference | MX Server |
|---:|---|
| 1 | `aspmx.l.google.com` |
| 5 | `alt1.aspmx.l.google.com` |
| 5 | `alt2.aspmx.l.google.com` |
| 10 | `alt3.aspmx.l.google.com` |
| 10 | `alt4.aspmx.l.google.com` |

The preference value influences the order in which mail delivery systems select mail servers: **the lower the value, the higher the preference**.

In this result, `aspmx.l.google.com` has the lowest numerical preference (`1`), followed by the servers with preference `5` and then those with preference `10`.

This query demonstrates how DNS records published for a domain can reveal information about its email infrastructure.

## Commands Used

The following commands were used during the activity:

```bash
sudo -i
host grancursos.com.br
host -t ns esr.rnp.br
host -t ns grancursosonline.com.br
host -t mx grancursosonline.com.br
```

## Concepts Practiced

### DNS

The **Domain Name System (DNS)** associates domain names with different types of information, including IP addresses, name servers, and mail servers.

### `host`

The `host` utility is a command-line tool used to perform DNS queries.

Examples from the activity:

```bash
host domain
host -t ns domain
host -t mx domain
```

### A Record

Maps a domain name to an IPv4 address.

### AAAA Record

Maps a domain name to an IPv6 address.

### NS Record

Identifies name servers associated with a domain.

### MX Record

Identifies mail servers responsible for receiving email for a domain, together with their preference values.

### HTTPS/SVCB Service Binding Records

Provide service-related information that can help clients discover protocol capabilities and connection parameters advertised through DNS.

### Passive DNS Enumeration

DNS enumeration can support reconnaissance by collecting publicly published domain information without directly exploiting the services associated with the domain.

The returned information represents the results of the particular DNS queries performed during the laboratory activity, not a guarantee of the domains' current configurations.

## Results

The activity provided practical experience using `host` to query different types of DNS information published for domain names.

The following types of records and information were examined:

- IPv4 addresses (`A` records).
- IPv6 addresses (`AAAA` records).
- Name servers (`NS` records).
- Mail servers (`MX` records).
- Additional information associated with HTTP services.

The exercise demonstrated how DNS queries can be used for **passive enumeration and reconnaissance**, helping analysts understand publicly available information about domain infrastructure without exploiting the associated services.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 11–12.

**Recorded screenshot:** Step 5 of the activity, as required by the laboratory instructions, showing the MX record query performed with `host`.

[View Evidence — Classes 11–12](../evidencias.pdf)

---

[Back to Classes 11–12](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
