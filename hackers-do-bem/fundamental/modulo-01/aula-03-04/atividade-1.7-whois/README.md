# Activity 1.7 — Exploring WHOIS on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 03–04  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use the `whois` tool to retrieve publicly available domain registration information and examine details such as the responsible organization, technical contact identifiers, and DNS name servers.

Three domain names were queried to compare the registration information returned by the WHOIS service.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** WHOIS
- **Related registry service:** Registro.br

## Procedure

### 1. Open an Administrative Shell

The terminal was opened and the following command was used to switch to the administrator account:

```bash
sudo -i
```

**Note:** Administrative privileges are generally unnecessary for standard WHOIS queries.

### 2. Query `esr.rnp.br`

The first lookup was performed using:

```bash
whois esr.rnp.br
```

The response included registration information associated with the `rnp.br` domain zone, including:

- Organization associated with the registration
- Owner and technical contact identifiers
- Name servers (DNS)
- IPv4 and IPv6 addresses associated with the name servers, where provided
- Registration creation and modification dates
- Domain registration status

The following fields were among those observed:

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

The `nserver` field identifies the name servers associated with the domain registration. These servers participate in DNS resolution for the corresponding domain.

### 3. Query `guanambi.ba.gov.br`

A second query was performed for a government domain:

```bash
whois guanambi.ba.gov.br
```

The response returned registration information associated with the `ba.gov.br` domain zone, including the organization responsible for the registration and the configured name servers.

The following fields were also observed:

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

This lookup demonstrated how a query for a subdomain can return registration information for its parent domain zone rather than a separate record for the exact hostname.

### 4. Query `itapaje.ce.gov.br`

The third query was performed using:

```bash
whois itapaje.ce.gov.br
```

The response included registration information associated with the `ce.gov.br` domain zone, such as:

- Organization associated with the registration
- Owner identifier
- Technical contact identifier
- DNS name servers
- IPv4 and IPv6 addresses, where provided
- Registration-related dates
- Domain registration status

This was the primary lookup used as evidence for the activity.

## Commands Used

```bash
sudo -i

whois esr.rnp.br

whois guanambi.ba.gov.br

whois itapaje.ce.gov.br
```

## Interpreting the Results

WHOIS is a query protocol used to retrieve registration information for domains and other Internet resources. The information returned depends on the registry, registrar, queried domain, and applicable disclosure policies.

The following fields were examined during the activity:

| Field | Meaning |
| --- | --- |
| `domain` | Domain name or registration zone |
| `owner` | Organization or entity associated with the registration |
| `owner-c` | Identifier for the owner contact record |
| `tech-c` | Identifier for the technical contact record |
| `nserver` | Name servers associated with the registration |
| `created` | Registration creation date |
| `changed` | Date of the last recorded modification |
| `status` | Registration status |

The exact fields and their availability can vary between WHOIS responses.

The information obtained can support reconnaissance and Open-Source Intelligence (OSINT) by helping analysts understand the public registration information and DNS infrastructure associated with a domain.

**Technical distinction:** WHOIS registration data and DNS records serve different purposes. WHOIS provides registration-related information, while DNS queries can be used to investigate records such as `A`, `AAAA`, `MX`, and `NS`. The two approaches can complement each other during reconnaissance.

## Result

WHOIS queries were performed against three domain names, and the publicly available registration information was examined.

The activity provided practical experience in identifying:

- Domain registration information
- Organizations associated with domain registrations
- Contact records referenced by identifiers
- DNS name servers
- IP addresses associated with name servers, where returned
- Registration dates and status information

## Concepts Practiced

- WHOIS
- Open-Source Intelligence (OSINT)
- Passive reconnaissance
- Domain registration
- Domain Name System (DNS)
- Name servers
- Public infrastructure information
- Asset reconnaissance
- Interpretation of registration records

## Evidence

The activity evidence is included in the PDF for Classes 03–04.

The relevant screenshot documents the WHOIS query for `itapaje.ce.gov.br` and the registration information returned by the service.

[View Evidence — Classes 03–04](../evidencias.pdf)

---

[Back to Classes 03–04](../) · [Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
