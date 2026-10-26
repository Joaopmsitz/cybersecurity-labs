# Activity 5.02 — Configuring the Active Directory Domain Controller

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 17–18  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Promote the Windows Server 2022 server to an Active Directory Domain Controller (DC), creating a new forest and configuring the domain's DNS.

This activity also includes creating a Reverse Lookup Zone for the network used in the laboratory.

## Environment

- Windows Server 2022
- Active Directory Domain Services
- Domain Controller
- DNS Server
- DNS Manager
- **Domain:** `aluno.hacker.com`
- **NetBIOS name:** `ALUNO`
- **Laboratory network:** `192.168.98.0/24`

## Procedure

### 1. Start the Server Promotion Process

After AD DS was installed in the previous activity, Server Manager displayed a notification indicating that additional configuration was required.

In the upper-right corner, the notification icon was selected, followed by:

```text
Promote this server to a domain controller
```

The Active Directory Domain Services configuration wizard was launched.

### 2. Create a New Forest

On the **Deployment Configuration** screen, the following option was selected:

```text
Add a new forest
```

The following value was entered in the **Root domain name** field:

```text
aluno.hacker.com
```

The wizard was then advanced to the next step.

### 3. Configure the Directory Services Restore Mode Password

On the **Domain Controller Options** screen, a password was configured for:

```text
Directory Services Restore Mode (DSRM)
```

The same password was entered in the **Password** and **Confirm Password** fields.

The password used in the laboratory is not recorded in this README.

After configuring the password, the wizard was advanced to the next steps.

### 4. Verify the NetBIOS Name

On the **Additional Options** screen, the domain's NetBIOS name was verified.

The displayed value was:

```text
ALUNO
```

The wizard was advanced through the remaining steps until the prerequisite checks were reached.

### 5. Check the Prerequisites

On the **Prerequisites Check** screen, the validation results were reviewed.

Windows Server displayed a green indicator and the following message:

```text
All prerequisite checks passed successfully....
```

After validation, the following option was selected:

```text
Install
```

The installation process began configuring the domain and promoting the server to a Domain Controller.

After completion, the server restarted automatically.

### 6. Access the Server Again

After waiting for Windows Server to start, the RDP connection was re-established using:

```text
192.168.98.20
```

Access was performed using the laboratory's administrative account.

After authentication, Server Manager was opened again.

The availability of the domain-related services was verified, including:

```text
AD DS
DNS
File and Storage Services
```

### 7. Open DNS Manager

In Server Manager, the following menu path was selected:

```text
Tools
    ↓
DNS
```

In DNS Manager, the following tree was expanded:

```text
DC01
└── Forward Lookup Zones
    └── aluno.hacker.com
```

The domain's forward lookup zone was available.

### 8. Create the Reverse Lookup Zone

In DNS Manager, the following item was selected:

```text
Reverse Lookup Zones
```

The item was right-clicked, and the following option was selected:

```text
New Zone...
```

The wizard was advanced using the options specified by the laboratory instructions.

The following value was entered in the **Network ID** field:

```text
192.168.98
```

The wizard was completed by selecting:

```text
Finish
```

The reverse lookup zone then appeared under **Reverse Lookup Zones**.

### 9. Verify the Reverse Lookup Zone

The newly created zone was opened:

```text
Reverse Lookup Zones
└── 98.168.192.in-addr.arpa
```

This configuration represents the network:

```text
192.168.98.0/24
```

Creating a reverse lookup zone allows DNS queries to start with an IP address and retrieve associated name information when the relevant reverse DNS records exist.

The evidence requested by the laboratory corresponds to this step.

### 10. Verify the Start of Authority Record

Within the zone:

```text
98.168.192.in-addr.arpa
```

the following item was opened:

```text
Start of Authority (SOA)
```

In the window that opened, the following tab was selected:

```text
Name Servers
```

The server was selected, and the following option was used:

```text
Edit...
```

The following option was then selected:

```text
Resolve
```

The server displayed the resolution result with a green success indicator.

### 11. Update the PTR Record

Still in DNS Manager, the forward lookup zone was accessed:

```text
DC01
└── Forward Lookup Zones
    └── aluno.hacker.com
```

The `dc01` server record was selected.

In the properties window, the following option was enabled:

```text
Update associated pointer (PTR) record
```

The change was confirmed.

### 12. Verify the Record in the Reverse Lookup Zone

Finally, the following zone was accessed again:

```text
Reverse Lookup Zones
└── 98.168.192.in-addr.arpa
```

The **Refresh** button was used to update the displayed information.

After refreshing the view, a new entry associated with the server's IP address appeared.

## Concepts Practiced

### Domain Controller

A Domain Controller is a server responsible for providing the central authentication and domain management services of Active Directory.

In this activity, `DC01` was promoted to a Domain Controller for:

```text
aluno.hacker.com
```

### Forest

A forest is the highest-level structure in Active Directory. It groups one or more domains and shares elements such as the directory schema and configuration.

In this activity, a new forest was created using the option:

```text
Add a new forest
```

### DNS Forward Lookup Zone

A forward lookup zone is used to resolve names to IP addresses.

In the laboratory, the following domain was configured as a forward lookup zone:

```text
aluno.hacker.com
```

### Reverse Lookup Zone

A reverse lookup zone supports DNS queries that start with an IP address and retrieve an associated name when a corresponding record is available.

For the laboratory network, the following zone was created:

```text
98.168.192.in-addr.arpa
```

It corresponds to the network:

```text
192.168.98.0/24
```

### PTR Record

A PTR (Pointer) record is used in reverse DNS lookups to associate an IP address with a name.

The following option enables the update of the associated PTR record:

```text
Update associated pointer (PTR) record
```

### SOA Record

The Start of Authority (SOA) record contains administrative information about a DNS zone, including information about the authoritative server and parameters used to maintain the zone.

## Results

The `DC01` server was promoted to a Domain Controller, and a new forest was created using the domain:

```text
aluno.hacker.com
```

The reverse DNS zone was also configured:

```text
98.168.192.in-addr.arpa
```

This zone corresponds to the network `192.168.98.0/24`.

Finally, the server's name resolution was checked, and the option to update the PTR record associated with the `DC01` IP address was enabled.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 17–18.

**Recorded screenshot:** Step 9 — creating and viewing the `98.168.192.in-addr.arpa` Reverse Lookup Zone.

[View Evidence — Classes 17–18](../evidencias.pdf)

---

[Back to Classes 17–18](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
