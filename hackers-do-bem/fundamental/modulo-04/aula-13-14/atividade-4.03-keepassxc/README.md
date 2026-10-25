# Activity 4.03 — Credential Management with KeePassXC

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 13–14  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use KeePassXC to create a password-protected database and store a test credential.

The activity aimed to demonstrate how a password manager works, including creating a database in the `.kdbx` format, selecting an encryption algorithm, and storing authentication credentials.

## Environment

- **Operating system:** Kali Linux
- **Application:** KeePassXC
- **Database file:** `Senhas.kdbx`
- **Directory:** `/home/aluno/Documentos/`
- **Selected encryption algorithm:** AES 256-bit

## Procedure

### 1. Launch KeePassXC

The application was started from the terminal:

```bash
keepassxc
```

KeePassXC opened normally under the standard laboratory user account.

Administrative privileges were not required to use the application during this activity.

### 2. Create the Database

On the KeePassXC welcome screen, the option to create a new database was selected.

The following database name was defined:

```text
Pessoal
```

During the advanced encryption configuration, the following algorithm was selected:

```text
AES 256-bit
```

The database was then protected with a password defined specifically for the laboratory exercise.

**Security note:** The password used during the exercise is not reproduced in this README.

KeePassXC displayed a warning indicating that the selected password was considered weak. Since this was a controlled academic environment, the credential specified by the laboratory instructions was used only to complete the activity.

For real-world use, a strong, unique master password should be selected. A password manager protects stored credentials through its database encryption, but the security of the database also depends on how the master password and the database file are handled.

### 3. Save the Database

The database was saved in the following directory:

```text
/home/aluno/Documentos/
```

The file was named:

```text
Senhas.kdbx
```

The `.kdbx` extension identifies the database format used by KeePassXC.

After creation, the database was available for storing credentials.

### 4. Create a Test Credential

A new entry was created inside the `Pessoal` database to represent a service account.

The fields used in the laboratory were:

| Field | Value used |
|---|---|
| Title | `Netflix` |
| Username | Test credential |
| Password | Test credential |
| URL | `https://www.netflix.com` |

The entry was saved in the database.

The purpose was to demonstrate how KeePassXC organizes authentication information in a single protected database.

The credentials used in the exercise were laboratory test data and are not reproduced in this README.

### 5. View the Stored Credential

After saving the entry, it was selected in KeePassXC to verify the stored information.

The following entry was displayed:

```text
Netflix
```

Its corresponding authentication fields were also available for inspection.

This step demonstrated how KeePassXC functions as a centralized credential repository, allowing usernames, passwords, and URLs to be stored in a protected database.

### 6. Delete the Test Entry

After validating the entry, the test credential was deleted from the database.

This step avoided retaining an unnecessary test credential in the activity database.

The database was subsequently closed.

### 7. Remove the Database File

After closing KeePassXC, the directory used to save the database was accessed:

```bash
cd /home/aluno/Documentos
```

The directory contents were then checked:

```bash
ls
```

The file created during the activity was identified:

```text
Senhas.kdbx
```

The file was then removed:

```bash
rm Senhas.kdbx
```

The removal was performed only after the activity had been completed.

**Note:** The `rm` command removes the file's directory entry; it does not guarantee secure erasure of all underlying data from storage media.

## Commands and Tools Used

The following commands were used during the activity:

```bash
keepassxc
cd /home/aluno/Documentos
ls
rm Senhas.kdbx
```

The database was created, configured, and managed through the KeePassXC graphical interface.

## Concepts Practiced

### KeePassXC

KeePassXC is a password manager that stores credentials in an encrypted database.

### KDBX Database

The `.kdbx` format is used by KeePassXC to store password databases and their associated entries.

### AES-256

AES (Advanced Encryption Standard) is a symmetric encryption algorithm. The 256-bit key variant was selected during the laboratory exercise.

Selecting AES-256 does not, by itself, guarantee the security of a password database. The overall protection also depends on the master password, database settings, and secure handling of the file.

### Credential Management

A password manager centralizes credentials instead of requiring users to store passwords in plain-text files or manually reuse them across different services.

### Master Password

The master password is used to unlock the protected database. It should be strong, unique, and kept confidential.

### Secure Handling of Test Credentials

The activity demonstrated the creation, inspection, and removal of a test credential. Using non-production credentials in training environments helps prevent accidental exposure of real account information.

## Results

The activity demonstrated how to create and use a credential database in KeePassXC.

The following tasks were completed:

- Launched KeePassXC.
- Created a database.
- Selected the AES 256-bit encryption algorithm.
- Protected the database with a password.
- Created a credential entry.
- Viewed the stored information.
- Deleted the test entry.
- Removed the `.kdbx` file at the end of the laboratory exercise.

The exercise demonstrated how a password manager can organize credentials in a centralized, encrypted database.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 13–14.

**Recorded screenshot:** Step 10 of the activity, as required by the laboratory instructions, showing the test credential stored in KeePassXC.

[View Evidence — Classes 13–14](../evidencias.pdf)

---

[Back to Classes 13–14](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
