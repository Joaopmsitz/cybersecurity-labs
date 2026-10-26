# Activity 5.07 — Creating an Organizational Unit (OU) in Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 19–20  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Create an Organizational Unit (OU) in Active Directory and add a new user within that structure.

In this activity, an OU named `TI` was created in the `aluno.hacker.com` domain, and a user named `usuarioti` was created inside it.

The exercise demonstrates the use of Organizational Units (OUs) and the Common Name (CN) in organizing Active Directory objects.

## Environment

- Windows Server 2022 — server / Domain Controller
- Active Directory Users and Computers
- **Domain:** `aluno.hacker.com`
- **Created OU:** `TI`
- **Created user:** `usuarioti`
- **User's name:** `Usuario TI`

## Procedure

### 1. Access Windows Server 2022

An RDP connection was established to the Windows Server 2022 server:

```text
192.168.98.20
```

Access was performed using a domain administrative account.

The credentials used in the laboratory are not recorded in this README.

### 2. Open Active Directory Users and Computers

The following search field was used on the taskbar:

```text
Type here to search
```

The following application was searched for:

```text
Active Directory Users and Computers
```

The application was opened from the search results.

### 3. Locate the Domain

In the left pane of Active Directory Users and Computers, the following domain was located:

```text
aluno.hacker.com
```

The domain was selected to view the existing Active Directory objects.

### 4. Create the Organizational Unit

The following domain was right-clicked:

```text
aluno.hacker.com
```

The following options were selected:

```text
New
    ↓
Organizational Unit
```

In the dialog that appeared, the following name was entered:

```text
TI
```

The operation was confirmed using:

```text
OK
```

The new OU then appeared in the domain structure.

### 5. Verify the Created OU

In the left pane of Active Directory Users and Computers, the structure now displayed:

```text
aluno.hacker.com
└── TI
```

The `TI` OU would be used to organize the user created in this activity.

### 6. Create a User Inside the OU

The following OU was selected:

```text
TI
```

It was right-clicked, and the following options were selected:

```text
New
    ↓
User
```

The new user creation dialog opened.

### 7. Enter the User Information

The following identification fields were completed:

```text
First name:
Usuario

Last name:
TI
```

In the following field:

```text
User logon name
```

the value below was entered:

```text
usuarioti
```

The value `usuarioti` is the logon name used by the new account. The user's displayed name is `Usuario TI`; in Active Directory, the Common Name (CN) is a directory object attribute and is not necessarily the same as the user logon name.

This is the step specified as the activity evidence.

### 8. Configure the Password

The following option was selected:

```text
Next
```

On the next screen, a password was configured according to the laboratory instructions.

The following option was unchecked:

```text
User must change password at next logon
```

The following option was also enabled:

```text
Password never expires
```

The password used in the laboratory is not recorded in this README.

**Security note:** The `Password never expires` setting was used as part of this laboratory exercise. In production environments, password expiration and credential management should follow the organization's security policy and applicable identity security guidance.

### 9. Finish Creating the User

The following options were selected:

```text
Next
    ↓
Finish
```

The user was successfully created inside the `TI` OU.

The resulting structure was similar to:

```text
aluno.hacker.com
└── TI
    └── Usuario TI
```

The user can subsequently be managed through Active Directory Users and Computers, where administrators can modify account properties, group membership, permissions, and other account-related settings.

## Concepts Practiced

### Organizational Unit (OU)

An Organizational Unit is an Active Directory object used to organize users, computers, and other objects within a logical structure.

OUs can also be used as scopes for applying and organizing Group Policy Objects (GPOs).

In this laboratory, the following OU was created:

```text
OU: TI
```

within the domain:

```text
aluno.hacker.com
```

### Common Name (CN)

The Common Name (CN) is an attribute used to identify an object within a directory's distinguished name.

In this exercise, the user was created with the display name:

```text
Usuario TI
```

and the logon name:

```text
usuarioti
```

These values serve different purposes in Active Directory and should not be assumed to be interchangeable.

### Active Directory Users and Computers

Active Directory Users and Computers (ADUC) is an administrative tool used to manage Active Directory objects, including:

- Users
- Groups
- Computers
- Organizational Units
- Account properties
- Group membership

### Created Structure

At the end of the activity, the domain organization was:

```text
aluno.hacker.com
└── TI
    └── Usuario TI
```

This structure allows objects to be separated according to departments or functions, making the environment easier to administer.

## Results

The `TI` Organizational Unit was created within the `aluno.hacker.com` domain.

The following user was then created inside that OU:

```text
Usuario TI
```

with the logon name:

```text
usuarioti
```

The activity demonstrated how to create and organize Active Directory objects using Active Directory Users and Computers.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 19–20.

**Recorded screenshot:** Step 9 — completing the creation of the `usuarioti` user inside the `TI` OU.

[View Evidence — Classes 19–20](../evidencias.pdf)

---

[Back to Classes 19–20](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
