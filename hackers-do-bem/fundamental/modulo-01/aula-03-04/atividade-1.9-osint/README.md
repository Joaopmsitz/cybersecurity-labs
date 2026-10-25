# Activity 1.9 — Conducting OSINT with Maltego

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 03–04  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use **Maltego** to conduct an Open-Source Intelligence (OSINT) investigation, starting with a public domain and applying different Transforms to identify related infrastructure, DNS information, people, email addresses, and mail servers.

The activity focused on passive reconnaissance using publicly available information associated with the domain under investigation.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** Maltego
- **Browser:** Firefox
- **Internet connection:** Required
- **Target domain:** `ufc.br`

## Procedure

### 1. Launch Maltego

Maltego was started from the terminal using:

```bash
maltego
```

After the application opened, a new project was created for the investigation.

### 2. Add the Domain to the Project

In the **Entity Palette**, the following entity type was selected:

```text
Infrastructure → Website
```

The `Website` entity was dragged onto the canvas.

Initially, Maltego displayed the example value:

```text
www.maltego.com
```

This value was replaced with:

```text
ufc.br
```

During this step, a certificate trust prompt appeared. The Cancel option was selected to continue with the laboratory exercise.

**Security note:** In real investigations, certificate trust warnings should be investigated before proceeding. Do not dismiss them without understanding their cause.

### 3. Identify Related Domains

With the `ufc.br` entity on the canvas, the context menu was opened by right-clicking the entity.

The following menu was selected:

```text
+ All Transforms
```

The following Transform was executed:

```text
[Utilities] To Domains [within Properties]
```

This Transform searches the entity's existing properties for possible domain names. The resulting entities were added to the graph for further analysis.

### 4. Identify DNS Names

The context menu was opened again, and the following Transform was executed:

```text
[Utilities] To DNSNames [within Properties]
```

This Transform searches the entity's properties for possible DNS names.

The results expanded the information displayed in the graph and demonstrated how existing entity properties can provide additional leads during an OSINT investigation.

**Technical distinction:** This is a property-extraction Transform, not a comprehensive DNS enumeration operation. Additional DNS-specific Transforms may be needed to retrieve or resolve DNS records.

### 5. Identify Potentially Related People

The following Transform was executed on the `ufc.br` entity:

```text
[Utilities] To Person [PGP]
```

This Transform searched public PGP key-server data for person names potentially associated with the domain.

The returned entities were displayed in the Maltego graph.

These results represent possible relationships found in the queried data source; they should not automatically be treated as verified employees or official representatives of the organization.

### 6. Identify Email Addresses

The following Transform was then executed:

```text
[Utilities] To Email Addresses [PGP]
```

The purpose was to identify email addresses associated with the domain through publicly available PGP information.

The results were added to the graph as new entities.

This step demonstrated how information from different entities and public data sources can be correlated during an OSINT investigation.

### 7. Identify Mail Servers

Finally, the following Transform was executed:

```text
[Utilities] To DNS Name - MX (mail server)
```

The objective was to identify the mail servers associated with the domain.

The results displayed mail servers associated with the analyzed domain. During this laboratory run, the returned servers were associated with Google's mail infrastructure.

**Technical note:** MX records identify the mail servers designated to receive email for a domain. The observed Google-related results document this exercise and should not be treated as confirmation of the domain's current mail configuration.

### 8. Analyze the Graph

After the Transforms had been executed, Maltego displayed entities associated with the `ufc.br` domain.

The graph was used to visualize the relationships investigated during the activity:

```text
Domain
  ├── Related domains
  ├── DNS names
  ├── Potentially related people
  ├── Email addresses
  └── MX mail servers
```

This visualization demonstrated one of Maltego's main capabilities: representing relationships between different entities in a graph.

The relationships and entities identified by individual Transforms should be validated against reliable sources before being used in a formal investigation.

### 9. Close the Application

After completing the analysis, Maltego was closed.

When prompted, the following option was selected:

```text
Discard All
```

The terminal was also closed after the activity.

## Commands Used

The only terminal command used to start the application was:

```bash
maltego
```

All remaining steps were performed through the Maltego graphical interface.

## Transforms Used

| Transform | Purpose |
| --- | --- |
| `[Utilities] To Domains [within Properties]` | Extract possible domain names from the entity's properties |
| `[Utilities] To DNSNames [within Properties]` | Extract possible DNS names from the entity's properties |
| `[Utilities] To Person [PGP]` | Search public PGP data for potentially related people |
| `[Utilities] To Email Addresses [PGP]` | Search public PGP data for associated email addresses |
| `[Utilities] To DNS Name - MX (mail server)` | Identify mail servers associated with the domain |

## Interpretation

The activity demonstrated how a single initial data point, in this case the `ufc.br` domain, can serve as the starting point for an OSINT investigation.

By applying different Maltego Transforms, the investigation expanded to include relationships between:

- Domain names
- DNS-related information
- Potentially related people
- Email addresses
- Mail servers
- Public infrastructure information

Using multiple data sources can provide a broader view of a target's publicly observable digital footprint without exploiting or modifying the investigated infrastructure.

However, discovered relationships are leads rather than definitive proof. Their accuracy depends on the source, the Transform used, and the available data.

## Result

A passive OSINT investigation was conducted in Maltego using `ufc.br` as the starting domain.

Multiple Transforms were executed to expand the graph and visualize relationships involving domain names, DNS-related entities, people, email addresses, and MX mail servers.

The activity provided practical experience in collecting, correlating, and visualizing publicly available information through an OSINT tool.

## Concepts Practiced

- Open-Source Intelligence (OSINT)
- Passive reconnaissance
- Maltego and Transforms
- Domain and DNS-related information
- MX records and mail infrastructure
- Public PGP key-server data
- Email address discovery
- Information correlation
- Infrastructure reconnaissance
- Validation of intelligence findings

## Evidence

The activity evidence is included in the PDF for Classes 03–04.

The screenshots document the Maltego graph and the results produced by the Transforms used during the investigation.

[View Evidence — Classes 03–04](../evidencias.pdf)

---

[Back to Classes 03–04](../) · [Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
