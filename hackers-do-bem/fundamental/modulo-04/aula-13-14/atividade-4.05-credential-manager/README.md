# Activity 4.05 — Windows Credential Manager

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 13–14  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Explore Windows Credential Manager in Windows Server 2022, identify the different types of stored credentials, and perform a credential backup procedure in a laboratory environment.

The activity also demonstrates the importance of protecting credential backup files, as they may contain sensitive authentication-related information.

## Environment

- **Operating system:** Windows Server 2022
- **Feature:** Credential Manager
- **Credential categories observed:**
  - Web Credentials
  - Windows Credentials
  - Certificate-based Credentials
  - Generic Credentials
- **Backup file:** `backup.cdr`

The credentials used to access the course environment are not reproduced in this README.

## Procedure

### 1. Open Credential Manager

After accessing Windows Server 2022 in the laboratory environment, the following feature was searched for:

```text id="1d7r2a"
Credential Manager
```

Credential Manager was then opened.

This Windows feature allows users to view and manage certain types of authentication information stored by the operating system.

### 2. Inspect Web Credentials

The **Web Credentials** section was opened to inspect the available credentials.

In the laboratory environment, this section could be empty.

This area relates to credentials used by certain Windows components and applications to authenticate to web resources.

The presence or absence of entries depends on the accounts, applications, and services used in the environment.

### 3. Inspect Windows Credentials

The **Windows Credentials** section was then opened.

The system displayed the following categories:

```text id="4ngh5x"
Windows Credentials
Certificate-based Credentials
Generic Credentials
```

#### Windows Credentials

These are related to credentials used to authenticate to certain Windows resources and services.

#### Certificate-based Credentials

These are related to authentication mechanisms that use certificates.

#### Generic Credentials

These are used by applications to store certain types of authentication information that do not necessarily fall into the Windows-specific credential category.

The available categories help distinguish different types of authentication information managed through Windows Credential Manager.

### 4. Start the Credential Backup

In the Credential Manager window, the following option was selected:

```text id="w0o8bi"
Back up Credentials
```

The backup wizard was launched.

The option to select the destination for the backup file was then used.

### 5. Specify the Backup File

In the wizard, the desktop was selected as the temporary storage location.

The filename entered was:

```text id="f04wz3"
backup
```

Windows added the appropriate extension to the backup file.

The resulting filename was:

```text id="5s19nr"
backup.cdr
```

**Security note:** The backup file is not included in this repository. It may contain sensitive authentication-related information and must be handled as confidential material.

### 6. Authenticate to Create the Backup

During the procedure, Windows requested additional authentication.

In the virtualized environment, the command equivalent to the following key combination was sent through the virtual machine's control toolbar:

```text id="7e7d7p"
Ctrl + Alt + Delete
```

The credentials for the account used in the laboratory were then entered to authorize the operation.

The credentials used to access the course environment are not included in this README.

### 7. Confirm the Backup

After authentication, the wizard continued creating the backup.

When the process finished, Windows displayed the following confirmation:

```text id="v4fbb1"
The backup was successful
```

This message indicates that the backup creation procedure completed successfully.

### 8. Verify the Backup File

The created file was located on the desktop:

```text id="qs82rp"
backup.cdr
```

This verification demonstrated that the backup file had been created in the selected location.

Because the file contains authentication-related material, it should not be uploaded to GitHub or shared publicly.

### 9. Clean Up the Laboratory Environment

After completing the activity, the backup file was removed from the laboratory environment.

Removing unnecessary copies of credential backups reduces the risk of unauthorized access to sensitive authentication information.

The file used during this activity was not included in the repository.

## Tools and Actions Used

The activity was performed through the Windows graphical interface. The main actions were:

```text id="2u1zfr"
Credential Manager
Back up Credentials
Ctrl + Alt + Delete
```

The backup was saved temporarily using the filename:

```text id="5qs5zm"
backup.cdr
```

The file was removed after the laboratory exercise was completed.

## Concepts Practiced

### Windows Credential Manager

Windows Credential Manager is a Windows component used to manage different types of credentials used by the operating system and applications.

### Windows Credentials

A category for credentials used to access certain Windows resources and services.

### Generic Credentials

A category for generic authentication information stored by applications and other components.

### Certificate-Based Credentials

A category associated with certificate-based authentication mechanisms.

### Credential Backup

Windows provides a way to back up certain credential information through Credential Manager.

This feature must be handled carefully because the resulting file contains authentication-related material and may be sensitive.

### Additional Authentication

The backup procedure required an additional authentication step before the operation could continue.

This demonstrates how Windows may request confirmation before performing sensitive credential-management operations.

## Security Considerations

The credential backup file created during this activity should not be committed to GitHub.

In a real environment, files of this type should be:

- Protected against unauthorized access.
- Stored only when necessary.
- Protected during transfer.
- Removed from temporary locations after use.
- Kept out of public repositories and other unauthorized sharing locations.

A successful backup does not make the backup file safe to disclose. Its contents should be treated as sensitive authentication material even after the original operation is complete.

The laboratory backup file was removed after the exercise.

## Results

The activity provided practical experience with Windows Credential Manager in Windows Server 2022 and the main credential categories presented by the feature.

The following tasks were completed:

- Located Credential Manager.
- Inspected Web Credentials.
- Inspected Windows Credentials.
- Identified Certificate-based Credentials.
- Identified Generic Credentials.
- Started the backup wizard.
- Created a temporary backup file.
- Authenticated the operation.
- Confirmed that the backup was created.
- Removed the backup file after completing the laboratory.

The exercise demonstrated that credential-management and backup mechanisms must be treated as sensitive components of system security.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 13–14.

**Recorded screenshot:** Step 11 of the activity, as specified in the overall Module 4 evidence list.

[View Evidence — Classes 13–14](../evidencias.pdf)

---

[Back to Classes 13–14](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
