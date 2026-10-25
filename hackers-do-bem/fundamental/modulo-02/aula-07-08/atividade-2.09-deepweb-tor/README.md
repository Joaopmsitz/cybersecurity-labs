# Activity 2.09 — Exploring the Deep Web Through Tor Browser

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 07–08  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use **Tor Browser** in a controlled educational environment to understand access to services available on the Tor network, examine the structure of `.onion` addresses, and distinguish the conventional Web from services accessible through the Tor network.

The activity followed the laboratory instructions and focused on understanding the technology without interacting with illegal content or services intended for criminal activities.

## Environment

- Kali Linux
- Firefox
- Tor Browser
- Tor network
- `.onion` services
- The Hidden Wiki

## Procedure

### 1. Access a Reference on the Conventional Web

Firefox was used to access the following website:

```text
https://thehiddenwiki.org
```

The page displayed a collection of addresses and services associated with the Tor network.

`.onion` addresses differ from conventional Internet domains. They identify services that are accessed through the Tor network.

### 2. Identify `.onion` Addresses

The page contained a list of addresses ending in:

```text
.onion
```

These addresses identify **Onion Services**, also known as onion services or hidden services.

Unlike conventional Internet domains, `.onion` addresses are resolved and accessed within the Tor network.

### 3. Access an Onion Service Through Tor Browser

Tor Browser was then used to access one of the `.onion` services provided in the course material.

The service was opened in a new Tor Browser tab after the browser had connected to the Tor network.

The address used during the laboratory exercise was an onion service supplied by the activity instructions. To avoid turning this documentation into a directory of active onion services, the address is not reproduced in this README.

### 4. Observe the Result

The accessed service displayed a page titled **The Hidden Wiki**, containing information about the service itself.

The following text was observed:

```text
The Hidden Wiki

The Original Hidden Wiki - Only @ [endereço onion do laboratório]

Update 07.2020: The old short v2 .onion hidden service links will no longer work after october 2021. We will list only v3 .onion's in the future.
```

The message referred to the transition from the older **Onion v2** address format to **Onion v3**.

The result demonstrated that Tor Browser could communicate with a service available through the Tor network during the laboratory session.

### 5. Onion Services

The laboratory also presented other `.onion` addresses as examples of services available through the Tor network.

The existence of an `.onion` address does not, by itself, mean that the content hosted by the service is legitimate or safe. For this reason, the activity remained within the educational scope defined by the course.

No interaction was performed with illegal marketplaces, criminal services, malware distribution, or other illicit content.

### 6. The Deep Web and the Tor Network

The term **Deep Web** generally refers to content that is not indexed by, or readily discoverable through, conventional search engines. Examples include private systems, databases, authenticated pages, and other resources that are not publicly indexed.

The Tor network is a different concept. It provides a privacy-oriented communications infrastructure and also supports services using `.onion` addresses.

The concepts are related, but they are not interchangeable:

- **Deep Web:** Content that is not necessarily indexed by conventional search engines.
- **Dark Web:** A term commonly used for services that rely on specialized technologies or networks for access.
- **Tor:** A network that routes communications through multiple relays and supports Onion Services.
- **`.onion`:** A special-use domain suffix associated with services accessed through the Tor network.

Not all Deep Web content is part of the Dark Web, and not every use of Tor involves accessing hidden or illicit content.

### 7. Onion Services

Onion Services are designed to be accessed through the Tor network.

Their characteristics include the use of `.onion` addresses and communication through Tor infrastructure, without requiring the service to be exposed in the same way as a conventional public web server.

This design provides privacy properties that differ from those of a traditional Web connection. However, it does not automatically establish that a service is trustworthy, secure, or anonymous in every respect.

### 8. Security Considerations

Access to the Tor network does not mean that every available service is safe.

When performing practical exercises involving Onion Services, it is important to:

- Stay within the authorized scope of the laboratory.
- Avoid services of unknown provenance.
- Avoid suspicious downloads.
- Never execute files obtained from untrusted sources.
- Avoid submitting personal information.
- Avoid interacting with illegal services.
- Close the session after completing the exercise.

In this activity, browsing was limited to understanding the technology and the structure of `.onion` services.

## Commands and Tools Used

The activity primarily used the graphical interfaces of Firefox and Tor Browser.

The conventional Web reference was:

```text
https://thehiddenwiki.org
```

Tor Browser was used to access an onion service supplied by the course instructions. Its address is intentionally omitted from this README.

## Results

The activity allowed me to:

1. Access a reference related to the Tor network through the conventional Web.
2. Identify the structure of `.onion` addresses.
3. Use Tor Browser to access an Onion Service.
4. Observe a page associated with The Hidden Wiki.
5. Identify the page's reference to Onion v2 and Onion v3 address formats.
6. Understand the relationship between Tor, the Deep Web, the Dark Web, and Onion Services.
7. Practice controlled browsing in an educational environment.

The main takeaway was that `.onion` services are part of the Tor network infrastructure and have different access characteristics from conventional websites.

## Evidence

The activity evidence is included in the PDF for Classes 07–08.

**Recorded screenshot:** Step 4 of the activity, as required by the laboratory instructions.

[View Evidence — Classes 07–08](../evidencia.pdf)

---

[Back to Classes 07–08](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
