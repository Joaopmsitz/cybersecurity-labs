# Activity 2.06 — Exploring File Encryption with Ccrypt on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 07–08  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Explore the Ccrypt command-line utility on Kali Linux to understand the process of encrypting and decrypting a file.

The activity demonstrates how a text file can be protected using an encryption key, making its contents unreadable while encrypted, and subsequently recovered using the correct key.

> **Safety notice:** This activity was performed exclusively for educational purposes in a laboratory environment. The password used was created specifically for the exercise.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tools:** Ccrypt and Nano
- **Execution environment:** Virtualized laboratory

## Procedure

### 1. Review Ccrypt

Before starting the hands-on exercise, the official Ccrypt project website was consulted to learn about the tool's purpose and functionality:

[Official Ccrypt Website](https://ccrypt.sourceforge.net/)

Ccrypt is a command-line utility designed to encrypt and decrypt files and data streams.

### 2. Open an Administrative Shell

The Kali Linux terminal was opened, and a superuser shell was started using:

```bash
sudo -i
```

### 3. Access the Documents Directory

The user's Documents directory was accessed:

```bash
cd /home/aluno/Documentos/
```

The contents of the directory were checked using:

```bash
ls
```

### 4. Create the Text File

The Nano text editor was used to create a file named `mensagem.txt`:

```bash
nano mensagem.txt
```

The following message was entered into the file:

```text
Hackers do bem!
```

The file was saved using `Ctrl + X`, followed by the confirmation requested by the editor.

### 5. Verify the Created File

After saving the file, the directory contents were listed again:

```bash
ls
```

The observed output was:

```text
mensagem.txt
```

The presence of `mensagem.txt` confirmed that the file had been created successfully.

At this stage, the file was still stored as plaintext, and its contents could be read normally.

### 6. Review the Ccrypt Help Output

Before encrypting the file, the available options were reviewed:

```bash
ccrypt -h
```

The following output was observed:

```text
ccrypt 1.11. Secure encryption and decryption of files and streams.

Usage: ccrypt [mode] [options] [file...]
       ccencrypt [options] [file...]
       ccdecrypt [options] [file...]
       ccat [options] file...

Modes:
    -e, --encrypt         encrypt
    -d, --decrypt         decrypt
    -c, --cat             cat; decrypt files to stdout
    -x, --keychange       change key
    -u, --unixcrypt       decrypt old unix crypt files

Options:
    -h, --help            print this help message and exit
    -V, --version         print version info and exit
    -L, --license         print license info and exit
    -v, --verbose         print progress information to stderr
    -q, --quiet            run quietly; suppress warnings
    -f, --force            overwrite existing files without asking
    -m, --mismatch        allow decryption with non-matching key
    -E, --envvar var      read keyword from environment variable (unsafe)
    -K, --key key         give keyword on command line (unsafe)
    -k, --keyfile file    read keyword(s) as first line(s) from file
    -P, --prompt prompt   use this prompt instead of default
    -S, --suffix .suf     use suffix .suf instead of default .cpt
    -s, --strictsuffix    refuse to encrypt files which already have suffix
    -F, --envvar2 var     as -E for second keyword (for keychange mode)
    -H, --key2 key        as -K for second keyword (for keychange mode)
    -Q, --prompt2 prompt  as -P for second keyword (for keychange mode)
    -t, --timid           prompt twice for encryption keys (default)
    -b, --brave           prompt only once for encryption keys
    -y, --keyref file     encryption key must match this encrypted file
    -r, --recursive       recurse through directories
    -R, --rec-symlinks    follow symbolic links as subdirectories
    -l, --symlinks        dereference symbolic links
    -T, --tmpfiles        use temporary files instead of overwriting (unsafe)
    --                    end of options, filenames follow
```

The following options were particularly relevant to the activity:

| Option | Purpose |
| --- | --- |
| `-e` | Encrypt a file |
| `-d` | Decrypt a file |
| `-c` | Decrypt a file and display its contents on standard output |
| `-x` | Change an encryption key |
| `-h` | Display the help message |
| `-V` | Display version information |
| `-v` | Display progress information |
| `-r` | Process directories recursively |

The help output provided an overview of Ccrypt's supported operations and configuration options.

### 7. Encrypt the File

With `mensagem.txt` created, the `-e` option was used to encrypt it:

```bash
ccrypt -e mensagem.txt
```

Ccrypt prompted for an encryption key:

```text
Enter encryption key:
Enter encryption key: (repeat)
```

A password created specifically for the laboratory was entered.

The `-e` option specifies encryption. After the operation completed, Ccrypt replaced the plaintext file with an encrypted version using the default `.cpt` suffix.

The resulting filename was:

```text
mensagem.txt.cpt
```

### 8. Verify the Encrypted File

This was the screenshot requested by the activity.

The directory contents were listed again:

```bash
ls
```

The observed output was:

```text
mensagem.txt.cpt
```

The `cat` command was then used to inspect the encrypted file directly:

```bash
cat mensagem.txt.cpt
```

The observed output was similar to:

```text
Z�w�.����K��^������>�I6E9Y�i��8Z;mU�\�;X�
```

The original message was no longer readable in the displayed output.

This demonstrated that the file contained encrypted data rather than the original plaintext message.

> **Note:** Unreadable or apparently random characters are expected when encrypted binary data is displayed directly as if it were a regular text file. Such output is not, by itself, a reliable way to validate encryption.

### 9. Decrypt the File

To recover the original file, the `-d` option was used:

```bash
ccrypt -d mensagem.txt.cpt
```

The tool requested the decryption key:

```text
Enter decryption key:
```

The same key used during encryption was entered.

The `-d` option specifies decryption, which reverses the encryption process when the correct key is provided.

The input file was:

```text
mensagem.txt.cpt
```

After successful decryption, the original filename was restored:

```text
mensagem.txt
```

### 10. Verify the Recovered File

The directory was listed again:

```bash
ls
```

The observed output was:

```text
mensagem.txt
```

The file contents were then displayed:

```bash
cat mensagem.txt
```

The output was:

```text
Hackers do bem!
```

The original message was recovered successfully, demonstrating that the encrypted file could be decrypted using the corresponding key.

### 11. Remove the Plaintext File

After the demonstration, the plaintext file was removed:

```bash
rm mensagem.txt
```

The directory contents were checked again:

```bash
ls
```

The file `mensagem.txt` was no longer present.

**Cleanup note:** This command removes the plaintext file only. It does not remove `mensagem.txt.cpt` if that encrypted file is still present. The encrypted copy should be handled separately if complete cleanup of the laboratory artifacts is required.

The terminal was closed after completing the activity.

## Commands Used

The principal commands executed during the activity were:

```bash
sudo -i
cd /home/aluno/Documentos/
ls
nano mensagem.txt
ccrypt -h
ccrypt -e mensagem.txt
ls
cat mensagem.txt.cpt
ccrypt -d mensagem.txt.cpt
ls
cat mensagem.txt
rm mensagem.txt
ls
```

## Activity Workflow

The process can be summarized as follows:

```text
mensagem.txt
     |
     | ccrypt -e
     v
mensagem.txt.cpt
     |
     v
Encrypted Data
     |
     | ccrypt -d
     v
mensagem.txt
     |
     v
Hackers do bem!
```

## Interpreting the Results

The activity demonstrated the practical use of file encryption to protect stored data.

Initially, the file contained the plaintext message:

```text
Hackers do bem!
```

After the following command was executed:

```bash
ccrypt -e mensagem.txt
```

the file was converted to an encrypted version with the `.cpt` suffix:

```text
mensagem.txt.cpt
```

Attempting to display the encrypted file using `cat` produced unreadable output, demonstrating that its contents were no longer available as ordinary plaintext.

The following command was then used to decrypt the file:

```bash
ccrypt -d mensagem.txt.cpt
```

After the correct key was provided, the original file was recovered, and its contents were displayed as:

```text
Hackers do bem!
```

The experiment illustrated the role of encryption in protecting data confidentiality. Encryption transforms readable information into ciphertext that should remain inaccessible to someone who does not possess the appropriate key.

It also demonstrated the difference between a plaintext file and its encrypted counterpart, identified by Ccrypt's default `.cpt` suffix.

## Result

The activity demonstrated how to:

- Review Ccrypt's available functions and options.
- Create a text file in Kali Linux.
- Enter a plaintext message.
- Inspect the command help output using `ccrypt -h`.
- Encrypt a file using `ccrypt -e`.
- Observe the conversion of `mensagem.txt` to `mensagem.txt.cpt`.
- Confirm that the encrypted contents were not readable as ordinary text.
- Decrypt the file using `ccrypt -d`.
- Recover and verify the original message.
- Remove the plaintext file after the demonstration.

The activity provided a practical example of how file encryption can be used as a technical control to protect data confidentiality.

## Concepts Practiced

- File encryption and decryption
- Ccrypt
- Data confidentiality
- Data at rest
- Encryption keys
- Ciphertext
- The `.cpt` file extension
- Linux command-line operations
- File handling and verification
- Technical security controls
- Data protection

## Evidence

The activity evidence is included in the PDF for Classes 07–08.

The relevant screenshot documents the Ccrypt encryption process and the appearance of the encrypted file.

[View Evidence — Classes 07–08](../evidencia.pdf)

---

[Back to Classes 07–08](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
