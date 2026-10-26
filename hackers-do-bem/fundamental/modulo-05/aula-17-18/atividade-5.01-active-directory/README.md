# Activity 5.01 — Installing Active Directory on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 17–18  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Install and prepare Active Directory Domain Services (AD DS) on Windows Server 2022, configuring the server that will subsequently be promoted to a Domain Controller.

This stage also installs the DNS-related role and the management tools required for the next activities.

## Environment

- Windows Server 2022
- Server Manager
- Active Directory Domain Services (AD DS)
- DNS Server
- Group Policy Management
- Remote Server Administration Tools

## Procedure

### 1. Access Windows Server 2022

The Windows Server 2022 virtual machine used in the laboratory was accessed through RDP.

- **IP address:** `192.168.98.20`
- **Username:** `Administrator`

The credentials used to access the server belong to the laboratory environment and are not recorded in this document.

After connecting, Server Manager was opened.

### 2. Rename the Server

In Server Manager, the following section was accessed:

```text
Local Server
```

The current computer name was selected, and the following option was opened:

```text
Change...
```

The computer name was changed to:

```text
DC01
```

After confirming the change, Windows Server was restarted to apply the new computer name.

After the restart, Server Manager was opened again to verify the change.

### 3. Add Server Roles

In the upper-right corner of Server Manager, the following options were selected:

```text
Manage
    ↓
Add Roles and Features
```

The installation wizard was started.

The initial steps were completed until the following screen was reached:

```text
Server Roles
```

### 4. Install Active Directory Domain Services

On the **Server Roles** screen, the following role was selected:

```text
Active Directory Domain Services
```

When the dialog requesting additional features appeared, the following option was selected:

```text
Add Features
```

This role provides the components required to configure the server as a Domain Controller in a subsequent step.

### 5. Install DNS Server

While still on the role selection screen, the following option was enabled:

```text
DNS Server
```

The following option was then selected:

```text
Add Features
```

The displayed dialog was confirmed, and the wizard continued to the next steps.

### 6. Verify Additional Features

On the **Features** screen, the options related to server management were reviewed.

These included:

```text
Group Policy Management
Remote Server Administration Tools
```

These components will be used later to administer the domain and manage Active Directory policies.

The wizard was advanced to the following stage:

```text
Confirmation
```

### 7. Install the Server Roles

On the **Confirmation** screen, the selected roles were reviewed.

The installation was started by clicking:

```text
Install
```

This was the stage specified by the laboratory instructions for the evidence screenshot.

After the installation began, the wizard displayed a progress bar indicating the installation status of the selected roles.

## Concepts Practiced

### Active Directory Domain Services (AD DS)

Active Directory Domain Services is the Windows Server directory service used to organize and manage resources in a domain-based network.

It enables centralized management of:

- Users
- Computers
- Groups
- Authentication
- Permissions
- Security policies

In this activity, AD DS was installed, but the server had not yet been promoted to a Domain Controller. That operation is covered in Activity 5.02.

### Domain Controller

A Domain Controller (DC) is a server running the services required to authenticate users and administer an Active Directory domain.

Installing AD DS is a prerequisite for promoting a server to a Domain Controller.

### DNS

The Domain Name System (DNS) translates domain and host names into information used by network devices.

In Active Directory environments, DNS plays a fundamental role in locating domain services. For this reason, the DNS Server role was also installed during this activity.

### Group Policy Management

Group Policy Management provides tools for creating and administering Group Policy Objects (GPOs).

GPOs will be used later in the laboratory to apply security settings and policies to domain users and computers.

## Results

Windows Server 2022 was prepared to serve as part of the Active Directory infrastructure.

The following roles were selected for installation:

```text
Active Directory Domain Services
DNS Server
```

The additional management tools required for subsequent activities were also reviewed in the installation wizard.

The server was renamed:

```text
DC01
```

The next activity will use this installation to promote the server to a Domain Controller and create a new Active Directory forest.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 17–18.

**Recorded screenshot:** Step 9 — the installation wizard's **Confirmation** screen, before the server roles were installed.

[View Evidence — Classes 17–18](../evidencias.pdf)

---

[Back to Classes 17–18](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
