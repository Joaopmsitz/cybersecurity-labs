# Activity 11.4 - ZIP Password Recovery with fcrackzip

## Overview

This activity uses fcrackzip to perform a brute-force password recovery test against the course-provided `radicals.zip` archive.

The practical exercise uses a lowercase character set and the password length specified by the course command.

## Objectives

- Examine the supplied encrypted ZIP archive.
- Configure a brute-force password search.
- Restrict the character set to lowercase letters.
- Validate candidate passwords against the archive.
- Identify the password reported by the tool.

## Environment

| Component | Description |
|---|---|
| Password Recovery Tool | fcrackzip |
| Archive | `radicals.zip` |
| Search Mode | Brute force |
| Character Set | Lowercase letters |
| Candidate Length | 5 characters |
| Course Result | `anarc` |

## Procedure

### 1. Run the Brute-Force Search

Execute the command supplied by the course:

```bash
fcrackzip -b -c 'a' -l '5' -u radicals.zip
```

The command uses the following options:

| Option | Purpose |
|---|---|
| `-b` | Select brute-force mode |
| `-c 'a'` | Use lowercase letters |
| `-l '5'` | Apply the specified password length setting |
| `-u` | Validate candidates by attempting to decompress the archive with unzip |

### 2. Review the Result

The course exercise identifies the recovered password:

```text
PASSWORD FOUND!!!!: pw == anarc
```

## Expected Result

fcrackzip reports the candidate password `anarc` as the recovered password for the supplied ZIP archive.

## Evidence

**Required screenshot: Print 4 - PDF page 4.**

The terminal screenshot must show:

- The personalized terminal prompt.
- The complete fcrackzip command.
- The output confirming the recovered password `anarc`.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- fcrackzip supports brute-force and dictionary-based ZIP password recovery.
- The `-c` option defines the candidate character set.
- The `-l` option controls password length parameters.
- The `-u` option uses unzip to help validate candidate passwords and reduce false positives.
- Password recovery must be restricted to course-provided files or archives for which authorization has been granted.
- Do not publish the archive or recovered password if it contains private or confidential data.

## References

- [fcrackzip - Debian Manual](https://sources.debian.org/src/fcrackzip/1.0-8/fcrackzip.1)
- [Kali Linux - fcrackzip](https://www.kali.org/tools/fcrackzip/)

## Navigation

- [Class 01 - Aula 11](../README.md)
- [Previous Activity - 11.3](../atividade-11.3-john-the-ripper/README.md)
- [Next Activity - 11.5](../atividade-11.5-esteganografia-steghide/README.md)
