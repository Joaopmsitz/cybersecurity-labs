# Activity 5.04 — Configuring a Windows Server 2022 Domain Client

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 17–18  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Configure a second Windows Server 2022 instance as an Active Directory domain client, using `DC01` as its DNS server and Domain Controller.

At the end of the activity, the client will be joined to the `aluno.hacker.com` domain, and a remote session will be established using the user created in Active Directory.

## Environment

- Windows Server 2022 — server / Domain Controller
- Windows Server 2022 — client
- Active Directory Domain Services
- DNS
- Remote Desktop
- **Domain:** `aluno.hacker.com`
- **Server:** `192.168.98.20`
- **Client:** `192.168.98.30`
- **Domain user:** `nome1`

## Procedure

### 1. Check the Server IP Address

With the Windows Server 2022 server connected, Command Prompt was opened by searching for:

```text
cmd
```

The following command was executed:

```cmd
ipconfig
```

**Relevant output observed in the laboratory:**

```text
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : ec2.internal
   Link-local IPv6 Address . . . . . : fe80::858e:1f4d:6a2:81ef%7
   IPv4 Address. . . . . . . . . . . : 192.168.98.20
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.98.1
```

The address `192.168.98.20` belongs to the server that provides domain and DNS services to the client.

### 2. Access the Windows Server 2022 Client

The RDP session connected to the server was minimized, and a new connection was established to the second Windows Server 2022 instance:

- **IP address:** `192.168.98.30`

The initial access was performed using the laboratory's administrative account.

The following procedures were carried out on the Windows Server 2022 client.

### 3. Test Connectivity to the Domain Controller

On the client, Command Prompt was opened, and the following command was executed:

```cmd
ping 192.168.98.20
```

**Observed output from the laboratory:**

```text
C:\Users\Administrator>ping 192.168.98.20

Pinging 192.168.98.20 with 32 bytes of data:
Reply from 192.168.98.20: bytes=32 time=1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.98.20:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

The result demonstrates that the client could reach the server over the network, with no packet loss:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### 4. Configure the Client DNS Settings

On the client, the following navigation path was used:

```text
Control Panel
    ↓
Network and Internet
    ↓
Network and Sharing Center
```

The Ethernet connection was opened, followed by the **Internet Protocol Version 4 (TCP/IPv4)** settings.

The following option was selected:

```text
Use the following DNS server addresses
```

The preferred DNS server was configured as:

```text
192.168.98.20
```

This address corresponds to `DC01`, which provides the DNS service used by the domain.

The changes were confirmed, and the windows were closed.

### 5. Install Remote Assistance

In Server Manager, the following options were selected:

```text
Manage
    ↓
Add Roles and Features
```

The wizard was advanced to the **Features** screen.

The following feature was enabled:

```text
Remote Assistance
```

The following options were then selected:

```text
Next
    ↓
Install
```

After the installation completed, the following option was selected:

```text
Close
```

### 6. Join the Client to the Domain

On the client, the advanced system settings were opened through:

```text
System
    ↓
Advanced system settings
```

In the **System Properties** window, the following tab was selected:

```text
Computer Name
```

The following option was selected:

```text
Change
```

Under the domain membership section, the following option was selected:

```text
Domain
```

The following domain name was entered:

```text
aluno.hacker.com
```

The credentials of the domain user created in the previous activity were requested.

The credentials used in the laboratory are not recorded in this document.

After authentication, Windows confirmed that the computer had joined the domain.

The displayed confirmation messages were acknowledged, and the system was restarted.

### 7. Configure Remote Access for the Domain User

After the restart, the following window was opened again:

```text
System Properties
    ↓
Remote
```

The option recorded in the laboratory was enabled:

```text
Allow connections only from...
```

The following option was then selected:

```text
Select Users...
```

The user selection process continued through:

```text
Add...
    ↓
Advanced...
    ↓
Find Now
```

The following account was located in the displayed list:

```text
Nome1 Sobrenome1
```

The user was selected and confirmed.

After the configuration, the domain user appeared in the list of users authorized for remote access.

### 8. Sign Out of the Administrative Session

After completing the configuration, the following options were used:

```text
Shut down or sign out
    ↓
Sign out
```

The administrative session was closed.

### 9. Establish a New RDP Connection

A new RDP connection was established to the client:

```text
192.168.98.30
```

The following domain user was used:

```text
nome1
```

The corresponding credentials belong to the laboratory environment and are not published in this README.

The previous RDP profile should not be reused because it contained the credentials of the administrative account used earlier.

During the connection, the following domain was selected:

```text
aluno.hacker.com
```

After authentication, the domain user successfully accessed the Windows Server 2022 client.

The evidence requested by the laboratory corresponds to this step.

## Concepts Practiced

### Domain Client

A computer joined to an Active Directory domain can use centralized services provided by the Domain Controller for authentication and management.

In this laboratory, the Windows Server 2022 client was joined to:

```text
aluno.hacker.com
```

### DNS and Active Directory

DNS plays a fundamental role in Active Directory operations.

For this reason, the client was configured to use the IP address of `DC01` as its DNS server:

```text
192.168.98.20
```

This allows the client to query DNS records used to locate domain services.

### Remote Desktop

The Remote Desktop Protocol (RDP) allows users to access a Windows computer remotely.

In this laboratory, remote access was configured to allow the domain user `nome1` to authenticate to the client.

### Domain Authentication

When a domain account is used, authentication is integrated with the Active Directory infrastructure.

The simplified workflow demonstrated in the activity was:

```text
Windows Client
      ↓
DNS → DC01
      ↓
aluno.hacker.com Domain
      ↓
User Authentication
      ↓
RDP Session
```

## Results

The Windows Server 2022 client was configured to use `DC01` as its DNS server and was subsequently joined to the domain:

```text
aluno.hacker.com
```

The user previously created in Active Directory was configured for remote access and used to establish a new RDP connection.

Authentication was performed with the domain account on the Windows Server 2022 client.

The activity demonstrated the relationship between DNS configuration, domain membership, user authorization, and remote authentication in an Active Directory environment.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 17–18.

**Recorded screenshot:** Step 10 — connecting to the Windows Server 2022 client through RDP using the domain user.

[View Evidence — Classes 17–18](../evidencias.pdf)

---

[Back to Classes 17–18](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
