# Activity 5.06 — Implementing Discretionary Access Control (DAC) on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 19–20  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Implement Discretionary Access Control (DAC) on the Windows Server 2022 client through file and folder permissions.

In this activity, the domain user `Nome1` was used to demonstrate how NTFS permissions can restrict access for the resource owner and subsequently restore access.

## Environment

- Windows Server 2022 — client
- Active Directory
- **Domain:** `aluno.hacker.com`
- **Client:** `192.168.98.30`
- **Domain user:** `ALUNO\nome1`
- **Resource:** `Documents` folder
- **File:** `Arquivo1.txt`

## Procedure

### 1. Access the Windows Server 2022 Client

An RDP connection was established to the Windows Server 2022 client:

```text
192.168.98.30
```

Access was performed using the domain user:

```text
ALUNO\nome1
```

The credentials used in the laboratory are not recorded in this README.

### 2. Create the Test File

After logging in, Notepad was opened using the search field:

```text
Type here to search
```

The following content was created:

```text
Teste
```

The file was saved as:

```text
Arquivo1.txt
```

in the following folder:

```text
Documents
```

After saving the file, Notepad was closed.

### 3. Locate the File in File Explorer

File Explorer was opened, and the following folder was accessed:

```text
Documents
```

The file:

```text
Arquivo1.txt
```

was located in the directory.

This file was used to demonstrate how access permissions work.

### 4. Open the Security Properties

The following folder was right-clicked:

```text
Documents
```

The following option was selected:

```text
Properties
```

In the properties window, the following tab was opened:

```text
Security
```

The main groups and users with permissions on the resource were identified, including:

```text
SYSTEM
Nome1
Administrators
```

### 5. Inspect Administrator Permissions

The following group was selected:

```text
Administrators
```

In the permissions area, the group had permissions marked under:

```text
Allow
```

These included permissions required to control the resource.

This step demonstrated that the administrative group had elevated permissions on the folder.

### 6. Attempt to Remove the Administrators Group

The following group was selected:

```text
Administrators
```

The following button was then used:

```text
Remove
```

Windows displayed a message preventing the removal.

The following option was selected:

```text
OK
```

The system retained the administrative group associated with the resource.

### 7. Deny Access to User Nome1

Next, the following user was selected:

```text
Nome1
```

In the permissions section, the following option was checked under **Deny**:

```text
Full control
```

The following option was selected:

```text
Apply
```

The warning was confirmed using the options presented by Windows, including:

```text
Yes
```

and:

```text
Continue
```

when prompted.

From this point onward, user `Nome1` was denied access to the `Documents` folder.

### 8. Verify the Access Restriction

File Explorer was reopened.

When attempting to access:

```text
Documents
```

the file:

```text
Arquivo1.txt
```

was no longer available to the user.

Access to the folder was also blocked because of the deny permission applied to the user.

### 9. Confirm the Access Denial

In File Explorer, another folder, such as:

```text
Downloads
```

was opened, and access to the following folder was attempted again:

```text
Documents
```

Windows displayed a message indicating that access had been denied.

The following option was selected:

```text
Continue
```

The system then requested administrative credentials to proceed.

After administrative authentication, the system continued to display the message:

```text
You have been denied permission to access this folder
```

The following option was selected:

```text
Close
```

This step demonstrated the practical effect of the `Deny` entry applied to the user.

### 10. Reopen the Folder Properties

The following folder was right-clicked:

```text
Documents
```

The following option was selected:

```text
Properties
```

The following tab was then opened again:

```text
Security
```

### 11. Restore the User's Permissions

The following user was selected:

```text
Nome1
```

The checkmarks under the following column were removed:

```text
Deny
```

The changes were applied using:

```text
Apply
```

and:

```text
Continue
```

until the warnings displayed by Windows were dismissed.

After the deny entries were removed, the user's access could be restored.

### 12. Verify Access Restoration

After restoring the permissions, another folder in File Explorer, such as:

```text
Downloads
```

was accessed, followed by:

```text
Documents
```

Access to the folder was permitted again.

The file:

```text
Arquivo1.txt
```

became accessible to the user once more.

This is the step specified as the activity evidence.

## Concepts Practiced

### Discretionary Access Control (DAC)

Discretionary Access Control (DAC) is an access control model in which permissions to a resource are defined for users and groups.

In Windows, permissions can be configured through the security properties of files and directories.

In this laboratory, access control was demonstrated directly on the following folder:

```text
Documents
```

using the user:

```text
Nome1
```

### Allow vs. Deny

Windows permissions include entries for:

```text
Allow
```

and:

```text
Deny
```

**Allow** grants a specified permission to a user or group.

**Deny** explicitly denies a specified permission.

In this activity, the following permission was configured:

```text
Nome1
    ↓
Deny
    ↓
Full control
```

This prevented the user from accessing the folder, even though the same user had created the file.

The deny entry was subsequently removed to restore access.

### Access Control Lists (ACLs)

Windows uses access control lists to define permissions for users and groups on files and directories.

The effective permissions depend on the applicable access control entries, group membership, and other security settings.

A deny entry can override otherwise applicable allow permissions for the same access right. Therefore, permission changes should be reviewed carefully to avoid unintended access restrictions.

### Demonstrated Concept

The laboratory demonstrates that access control does not depend solely on who created a file.

User `Nome1` created:

```text
Arquivo1.txt
```

However, an explicit permission rule was subsequently applied to the same user:

```text
Deny → Full control
```

As a result, access to the resource was blocked until the deny rule was removed.

## Results

A DAC scenario was implemented on the Windows Server 2022 client using the security permissions of the `Documents` folder.

Access for user `Nome1` was initially permitted, then denied through:

```text
Deny → Full control
```

and finally restored after the deny permissions were removed.

The test demonstrated how Windows access control lists (ACLs) can regulate user access to files and directories.

## Evidence

The activity evidence is included in the PDF for Module 05, Classes 19–20.

**Recorded screenshot:** Step 18 — accessing the `Documents` folder again after removing the `Deny` permissions.

[View Evidence — Classes 19–20](../evidencias.pdf)

---

[Back to Classes 19–20](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
