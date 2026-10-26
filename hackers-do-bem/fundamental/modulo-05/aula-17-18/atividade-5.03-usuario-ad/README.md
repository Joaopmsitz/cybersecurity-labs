# Activity 5.03 — Creating a Domain User in Active Directory

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 17–18  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Create a user in the Active Directory domain, add the user to the **Remote Desktop Users** group, and create a Group Policy Object (GPO) to allow domain users to log on through Remote Desktop Services.

## Environment

- Windows Server 2022
- Active Directory
- Active Directory Users and Computers
- Group Policy Management
- Group Policy Management Editor
- **Domain:** `aluno.hacker.com`
- **Created user:** `nome1`
- **Organizational Unit:** `Rede1`
- **GPO:** `Alunos`

## Procedure

### 1. Create the User in Active Directory

In Server Manager, the following menu path was accessed:

```text
Tools
    ↓
Active Directory Users and Computers
```

In the left pane, the following tree was expanded:

```text
aluno.hacker.com
└── Users
```

In the users area, the following options were selected:

```text
New
    ↓
User
```

The new user's information was entered:

```text
First name: Nome1
Last name: Sobrenome1
User logon name: nome1
```

A password was set for the user.

The password used in the laboratory is not recorded in this README.

The following option was unchecked:

```text
User must change password at next logon
```

The following option was enabled:

```text
Password never expires
```

After completing the wizard, the user **Nome1 Sobrenome1** appeared in the domain users list.

**Security note:** Disabling password expiration may be appropriate for a specific controlled lab exercise, but it should not be adopted as a general production policy without an explicit security requirement and compensating controls.

### 2. Add the User to Remote Desktop Users

After creating the user, the following properties were opened:

```text
Nome1 Sobrenome1
    ↓
Properties
```

On the following tab:

```text
Member of
```

the option below was selected:

```text
Add...
```

In the group selection dialog, the following term was searched for:

```text
remote
```

After selecting **Check Names**, the following group was selected:

```text
Remote Desktop Users
```

The change was confirmed using **OK**, followed by **Apply** and **OK**.

### 3. Open Group Policy Management

In Server Manager, the following menu path was accessed:

```text
Tools
    ↓
Group Policy Management
```

In the left pane, the following structure was expanded:

```text
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
```

### 4. Create the Organizational Unit

The following domain was right-clicked:

```text
aluno.hacker.com
```

The following option was selected:

```text
New Organizational Unit
```

The new organizational unit was named:

```text
Rede1
```

After confirming the operation, the `Rede1` OU appeared under the domain.

### 5. Create the GPO

The following OU was right-clicked:

```text
Rede1
```

The following option was selected:

```text
Create a GPO in this domain, and Link it here...
```

The policy was named:

```text
Alunos
```

After creation, the GPO appeared linked to the `Rede1` OU.

### 6. Edit the GPO

The following GPO was right-clicked:

```text
Alunos
```

The following option was selected:

```text
Edit...
```

In Group Policy Management Editor, the following path was followed:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── User Rights Assignment
```

The following policy was opened:

```text
Allow log on through Remote Desktop Services
```

### 7. Add Domain Users

In the policy window, the following option was enabled:

```text
Define these policy settings
```

The following selection path was then used:

```text
Add User or Group...
    ↓
Browse...
    ↓
Advanced
    ↓
Find Now
```

From the displayed list, the following group was selected:

```text
Domain Users
```

### 8. Add Authenticated Users

The user and group selection process was repeated:

```text
Advanced
    ↓
Find Now
```

The following group was selected:

```text
Authenticated Users
```

The changes were confirmed using:

```text
OK
OK
Apply
OK
```

This configured the policy to include the selected groups in the **Allow log on through Remote Desktop Services** user right.

**Security note:** Granting this right through broad groups such as `Domain Users` and `Authenticated Users` can expand remote logon access considerably. In production environments, restrict the policy to the specific users or groups that require Remote Desktop access, and ensure that the GPO is linked and scoped appropriately.

### 9. Update Group Policies

On the Windows taskbar, Command Prompt was opened by searching for:

```text
cmd
```

The following command was executed:

```cmd
gpupdate /force
```

**Output displayed in the laboratory:**

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

The evidence requested by the laboratory corresponds to this step.

The output confirms that the computer and user Group Policy update operations completed successfully. It does not, by itself, verify that every intended setting was applied to a particular user or computer; effective policy can be checked separately when needed.

## Concepts Practiced

### Active Directory Users and Computers

Active Directory Users and Computers (ADUC) is an administrative tool used to manage domain objects, such as:

- Users
- Groups
- Computers
- Organizational Units

In this activity, it was used to create the `nome1` user.

### Remote Desktop Users Group

The **Remote Desktop Users** group organizes users who are permitted to use certain remote access capabilities, subject to the system's effective permissions and policies.

The newly created user was added to this group during the activity.

Membership in this group alone does not guarantee successful remote access; the user must also satisfy the applicable logon rights and other security requirements.

### Group Policy Object (GPO)

A GPO is a collection of settings that can be applied to users and computers in a domain.

In this laboratory, the following GPO was created:

```text
Alunos
```

It was linked to the following OU:

```text
Rede1
```

### User Rights Assignment

The **User Rights Assignment** section defines rights granted to users and groups in Windows.

The policy used was:

```text
Allow log on through Remote Desktop Services
```

It controls which users or groups can be granted the right to log on through Remote Desktop Services. Effective access also depends on other applicable policies and security controls.

### `gpupdate /force`

The command:

```cmd
gpupdate /force
```

requests an immediate Group Policy update on the computer.

The `/force` option forces the reapplication of policy settings, including settings that do not appear to have changed since the previous update.

## Results

The following user was created:

```text
Nome1 Sobrenome1
```

in the domain:

```text
aluno.hacker.com
```

The user was added to the **Remote Desktop Users** group.

The following OU was also created:

```text
Rede1
```

And the following GPO was created and linked to that OU:

```text
Alunos
```

The **Allow log on through Remote Desktop Services** policy was configured to include `Domain Users` and `Authenticated Users`.

Finally, the `gpupdate /force` command reported successful computer and user policy updates:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

The activity demonstrated how to create a domain user, manage group membership, organize domain objects with an OU, configure a GPO, and request an immediate Group Policy update.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 17–18.

**Recorded screenshot:** Step 11 — executing `gpupdate /force` and confirming the policy update results.

[View Evidence — Classes 17–18](../evidencias.pdf)

---

[Back to Classes 17–18](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
