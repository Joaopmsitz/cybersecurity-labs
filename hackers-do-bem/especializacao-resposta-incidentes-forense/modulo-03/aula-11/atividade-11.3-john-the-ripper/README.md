# Activity 11.3 - Password Auditing with John the Ripper

## Overview

This activity uses John the Ripper to audit the password hashes supplied in the training environment.

The practical exercise uses a prepared `unshadow.txt` file and a wordlist to identify a weak password.

## Objectives

- Examine the supplied password hash file.
- Select the appropriate hash format.
- Perform a wordlist-based password audit.
- Verify the recovered password.

## Environment

| Component | Description |
|---|---|
| Password Auditing Tool | John the Ripper |
| Input File | `unshadow.txt` |
| Hash Format | `crypt` |
| Wordlist | `/usr/share/john/password.lst` |
| Exercise Result | `harrypotter` |

## Procedure

### 1. Run the Wordlist Audit

Execute the command supplied by the course:

```bash
john --format=crypt unshadow.txt --wordlist=/usr/share/john/password.lst
```

The command instructs John the Ripper to process the supplied file using the `crypt` format and the specified password wordlist.

### 2. Review the Results

John displays recovered passwords when a candidate matches a supplied hash.

The course exercise identifies the recovered password:

```text
harrypotter
```

The results can also be displayed with:

```bash
john --show --format=crypt unshadow.txt
```

## Expected Result

John the Ripper successfully identifies the weak password `harrypotter` from the supplied training hash data.

## Evidence

**Required screenshot: Print 3 - PDF page 3.**

The terminal screenshot must show:

- The personalized terminal prompt.
- The execution of the `john --format=crypt` command.
- The successful recovery of the password `harrypotter`.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- John the Ripper supports wordlist-based password auditing.
- The `--wordlist` option selects the candidate password file.
- The `--format` option forces the hash format.
- Support for `crypt` depends on the installed John build and platform.
- Password hash files and recovered passwords are sensitive artifacts. Do not commit `unshadow.txt`, raw password hashes, or recovered credential material to a public repository.
- Perform password auditing only on accounts and hash files for which authorization has been granted.

## References

- [John the Ripper - Official Documentation](https://www.openwall.com/john/doc/)
- [John the Ripper - Command-Line Options](https://www.openwall.com/john/doc/OPTIONS.shtml)
- [John the Ripper - Cracking Modes](https://www.openwall.com/john/doc/MODES.shtml)

## Navigation

- [Class 01 - Aula 11](../README.md)
- [Previous Activity - 11.2](../atividade-11.2-reconstrucao-fatos-autopsy/README.md)
- [Next Activity - 11.4](../atividade-11.4-senha-arquivo-zip-fcrackzip/README.md)
