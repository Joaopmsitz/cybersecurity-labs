# Activity 5.05 — Configuring a Password Policy GPO in Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 17–18  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Create and configure a Group Policy Object (GPO) to establish a password policy for the Active Directory domain.

This activity configures requirements related to password expiration, minimum length, complexity, and password history.

## Environment

- Windows Server 2022
- Active Directory
- Group Policy Management
- Group Policy Management Editor
- **Domain:** `aluno.hacker.com`
- **GPO:** `Politica de senhas`

## Procedure

### 1. Open Group Policy Management

The Windows Server 2022 server was accessed through RDP.

- **IP address:** `192.168.98.20`
- **Username:** `Administrator`

The credentials used belong to the laboratory environment and are not recorded in this document.

In Server Manager, the following menu path was accessed:

```text
Tools
    ↓
Group Policy Management
```

### 2. Locate the Domain

In the left pane of Group Policy Management, the following structure was expanded:

```text
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
```

The following folder was located within the domain:

```text
Group Policy Objects
```

### 3. Create the GPO

The following item was right-clicked:

```text
Group Policy Objects
```

The following option was selected:

```text
New
```

The new policy was named:

```text
Politica de senhas
```

After confirming the creation, the GPO appeared in the domain's list of policy objects.

The original Portuguese name was retained as configured in the laboratory.

### 4. Open the GPO Editor

The following GPO was right-clicked:

```text
Politica de senhas
```

The following option was selected:

```text
Edit
```

The **Group Policy Management Editor** window opened.

### 5. Locate the Password Settings

In the left pane, the following path was followed:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Password Policy
```

This section contains settings related to password management for the domain.

### 6. Configure Maximum Password Age

The following policy was opened:

```text
Maximum password age
```

The following option was enabled:

```text
Define this policy setting
```

The value was set to:

```text
120 days
```

The configuration was applied using:

```text
Apply
    ↓
OK
```

This setting defines the maximum period before a password must be changed.

### 7. Configure Minimum Password Length

The following policy was opened:

```text
Minimum password length
```

The setting was enabled and configured as:

```text
9 characters
```

After setting the value, the following options were selected:

```text
Apply
    ↓
OK
```

This setting establishes the minimum number of characters required for passwords.

### 8. Enable Password Complexity

The following setting was opened:

```text
Password must meet complexity requirements
```

The policy definition option was enabled, and the following value was selected:

```text
Enabled
```

The change was applied and confirmed.

With this setting enabled, Windows requires passwords to meet the system's password complexity rules.

### 9. Configure Password History

The following policy was opened:

```text
Enforce password history
```

The policy was enabled and configured with the value:

```text
3
```

This setting prevents the immediate reuse of previously used passwords by retaining password history for the configured number of passwords.

The change was applied and confirmed.

### 10. Link the GPO to the Domain

Back in Group Policy Management, the following domain was selected:

```text
aluno.hacker.com
```

The domain was right-clicked, and the following option was selected:

```text
Link an Existing GPO
```

From the list of available GPOs, the following policy was selected:

```text
Politica de senhas
```

The selection was confirmed using:

```text
OK
```

The GPO was then linked to the domain.

### 11. Update Group Policy

After linking the policy, Command Prompt was opened by searching for:

```text
cmd
```

The following command was executed:

```cmd
gpupdate /force
```

This command was used to force a Group Policy update.

### 12. Verify the Policy Update Result

The output displayed in the laboratory was:

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

The message confirms that the computer and user Group Policy update operations completed successfully.

The evidence requested by the laboratory corresponds to this step.

## Applied Configuration

The `Politica de senhas` GPO was configured with the following parameters:

| Setting | Value |
|---|---|
| Maximum password age | 120 days |
| Minimum password length | 9 characters |
| Password complexity | Enabled |
| Enforce password history | 3 passwords |

The GPO was linked to the following domain:

```text
aluno.hacker.com
```

## Concepts Practiced

### Group Policy Object (GPO)

A GPO is a collection of administrative settings that can be applied to users and computers in a Windows environment.

In an Active Directory domain, GPOs provide centralized management of various security and administrative settings.

### Password Policy

The Password Policy contains settings that define requirements for passwords used in the domain.

The following settings were configured in this activity:

- Maximum password age
- Minimum password length
- Password complexity
- Password history

### Password History

Password history prevents users from immediately reusing previous credentials.

In this laboratory, the policy was configured to retain a history of three passwords.

### Password Complexity

The password complexity setting establishes additional requirements for passwords, increasing the variety of characters required according to Windows rules.

### `gpupdate /force`

The command:

```cmd
gpupdate /force
```

forces a Group Policy refresh on the computer.

The output:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

indicates that the computer and user policy update operations completed successfully.

A successful refresh does not, by itself, prove that every intended setting is effective for every user. The resulting policy can be verified separately when necessary.

## Results

The following GPO was created:

```text
Politica de senhas
```

It was configured with the following requirements:

- Maximum password age of 120 days
- Minimum password length of 9 characters
- Password complexity enabled
- Password history set to 3 passwords

The GPO was linked to the `aluno.hacker.com` domain, and the Group Policy update command completed successfully.

The activity demonstrated how to create a GPO, configure domain password requirements, link the policy to a domain, and initiate a policy refresh using `gpupdate /force`.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 17–18.

**Recorded screenshot:** Step 12 — executing `gpupdate /force` and confirming the computer and user policy update results.

[View Evidence — Classes 17–18](../evidencias.pdf)

---

[Back to Classes 17–18](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
