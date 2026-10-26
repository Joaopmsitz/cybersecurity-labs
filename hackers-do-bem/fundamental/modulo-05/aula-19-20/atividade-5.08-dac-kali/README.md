# Activity 5.08 — Discretionary Access Control (DAC) on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 19–20  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity demonstrates Discretionary Access Control (DAC) on Kali Linux using traditional Linux file permissions.

The objective is to inspect the permissions initially assigned to a file and then modify them using the `chmod` command, granting the file owner read, write, and execute permissions.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Working directory:** `/home/aluno/Documentos/`

The credentials used in the laboratory are not recorded in this document.

## Procedure

### 1. Open the Terminal

After accessing the Kali Linux machine through RDP, the terminal was opened, and administrative access was obtained using:

```bash
sudo -i
```

The user's Documents directory was then accessed:

```bash
cd /home/aluno/Documentos/
```

### 2. Create the File

The `nano` editor was used to create the `texto.txt` file:

```bash
nano texto.txt
```

The following content was entered into the file:

```text
Teste1
```

The file was saved using:

```text
Ctrl + X
S
Enter
```

### 3. Verify the File

After saving the file, the `ls` command was used to confirm that it existed:

```bash
ls
```

**Observed output:**

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls
texto.txt
```

The output confirms that `texto.txt` was created in `/home/aluno/Documentos/`.

### 4. Inspect the Current Permissions

To view the file's detailed permissions, the following command was executed:

```bash
ls -l
```

**Observed output:**

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls -l
total 4
-rw-r--r-- 1 root root 7 fev 10 18:10 texto.txt
```

The output can be interpreted as follows:

```text
-rw-r--r-- 1 root root 7 fev 10 18:10 texto.txt
│││││││││
││││││││└── file
│││││││└─── permissions for other users
││││││└──── group permissions
│││││└───── owner permissions
```

The permission string:

```text
-rw-r--r--
```

represents:

- `-` — regular file.
- `rw-` — the owner has read and write permissions.
- `r--` — the group has read-only permission.
- `r--` — other users have read-only permission.

The output also shows that:

- The owner is `root`.
- The associated group is `root`.
- The file is 7 bytes in size.
- The filename is `texto.txt`.

### 5. Modify Permissions with `chmod`

To demonstrate discretionary access control, the following command was used:

```bash
chmod u+rwx texto.txt
```

The `chmod` command modifies access permissions for files and directories.

In this command:

- `u` — user, meaning the file owner.
- `+` — adds permissions.
- `r` — read permission.
- `w` — write permission.
- `x` — execute permission.
- `texto.txt` — the file whose permissions will be modified.

The command therefore adds read, write, and execute permissions for the file owner.

### 6. Verify the Updated Permissions

After executing `chmod`, the following command was run again:

```bash
ls -l
```

**Observed output:**

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls -l
total 4
-rwxr--r-- 1 root root 7 fev 10 18:10 texto.txt
```

The change can be observed in the permission string.

**Before:**

```text
-rw-r--r--
```

**After:**

```text
-rwxr--r--
```

The `x` permission was added for the owner. As a result, the `root` owner now has:

```text
rwx
```

This represents:

- Read
- Write
- Execute

The group and other users retain their previous permissions:

```text
r--
```

**Technical note:** Adding the execute permission sets the file's executable permission bit. It does not, by itself, make a plain text file into an executable program.

## Concepts Practiced

### DAC — Discretionary Access Control

Discretionary Access Control (DAC) is an access control model in which the owner of a resource has authority to define or modify access permissions.

In Linux, this model is primarily represented by permissions associated with:

- Owner (`user`/`owner`)
- Group (`group`)
- Other users (`others`)

### Linux File Permissions

The three basic permissions used in this activity are:

| Permission | Symbol | Meaning |
|---|---|---|
| Read | `r` | Allows reading |
| Write | `w` | Allows modification |
| Execute | `x` | Allows execution |

These permissions are organized into three groups:

```text
rwx rwx rwx
│   │   │
│   │   └── others
│   └────── group
└────────── owner
```

Each group has its own combination of read, write, and execute permissions.

### `chmod`

The `chmod` command is used to change file and directory permissions.

In this activity, the following command was used:

```bash
chmod u+rwx texto.txt
```

The command modified only the owner's permissions without changing those assigned to the group or other users.

## Results

The activity demonstrated how DAC works in Linux through traditional file permissions.

Initially, the file had the following permissions:

```text
-rw-r--r--
```

After executing:

```bash
chmod u+rwx texto.txt
```

the permissions became:

```text
-rwxr--r--
```

This change shows that the file owner was granted execute permission while retaining the read and write permissions already assigned.

The group and other users continued to have read-only access.

## Evidence

The evidence for this activity corresponds to Step 7, after executing `chmod` and verifying the updated permissions using `ls -l`.

[View Evidence — Classes 19–20](../evidencias.pdf)

---

[Back to Classes 19–20](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
