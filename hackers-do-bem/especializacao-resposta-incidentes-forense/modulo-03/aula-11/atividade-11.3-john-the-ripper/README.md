# Activity 11.3 — Password Hash Auditing with John the Ripper

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 01  
> **Course Lesson:** 11  
> **Environment:** Linux forensic environment  
> **Status:** Completed

## 1. Objective

Perform a wordlist-based password audit against the supplied Unix password hash data using John the Ripper.

The activity uses the prepared file `unshadow.txt` as input and the system wordlist located at:

```text
/usr/share/john/password.lst
```

The exercise demonstrates how password auditing can identify weak passwords in recovered authentication data.

The password recovered during the activity was:

```text
harrypotter
```

The exercise is limited to the password data supplied by the course for the forensic investigation.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | Linux |
| Password Auditing Tool | John the Ripper |
| Input File | `unshadow.txt` |
| Hash Format | `crypt` |
| Attack Mode | Wordlist |
| Wordlist | `/usr/share/john/password.lst` |
| Recovered Password | `harrypotter` |

The activity notes identify `unshadow.txt` as the prepared input file. The exact source paths of the original password and shadow files are not included in the supplied activity description.

## 3. Password Forensics Concepts

### Unix Password Storage

Unix-like systems traditionally store account information in `/etc/passwd` and protected password hashes in `/etc/shadow`.

The password database contains user account information, while the shadow database stores password-related fields that should not be exposed to ordinary users.

During a forensic investigation, copies of these files may be examined to identify weak credentials or suspicious account configuration.

### Unshadow

John the Ripper includes a utility called `unshadow` that can combine entries from passwd and shadow files into a format suitable for password auditing.

The activity uses the already prepared file:

```text
unshadow.txt
```

The file serves as the input for John the Ripper.

### John the Ripper

John the Ripper is a password security auditing tool.

It supports several password hash formats and multiple password candidate generation methods.

This activity uses wordlist mode, in which John tests candidate passwords from a supplied text file against the provided password hashes.

### Wordlist Mode

A wordlist is a text file containing candidate passwords, normally one candidate per line.

The tool processes the entries and checks whether any candidate produces a result matching the supplied hash.

The wordlist used in this exercise is:

```text
/usr/share/john/password.lst
```

### Password Hash Format

The command explicitly selects:

```text
crypt
```

This tells John to use its `crypt` format implementation when processing the supplied hashes.

The format must match the input data. Selecting an incompatible format can prevent successful hash interpretation.

## 4. Procedure

### Step 1 — Identify the Prepared Password File

The activity uses the file:

```text
unshadow.txt
```

This file contains the prepared account and password hash information used for the audit.

The wordlist supplied by the Linux environment is:

```text
/usr/share/john/password.lst
```

The two files have different purposes:

| File | Purpose |
|---|---|
| `unshadow.txt` | Input containing account and password hash records |
| `password.lst` | Candidate passwords used during the audit |

### Step 2 — Execute John the Ripper

The password audit was executed using:

```bash
john --format=crypt unshadow.txt --wordlist=/usr/share/john/password.lst
```

The command components are:

| Component | Function |
|---|---|
| `john` | Starts John the Ripper |
| `--format=crypt` | Selects the `crypt` password hash format |
| `unshadow.txt` | Input file containing the prepared password data |
| `--wordlist=` | Selects wordlist-based candidate testing |
| `/usr/share/john/password.lst` | Candidate password list |

John reads the input file, interprets the supported hash records, and tests candidate passwords from the specified wordlist.

### Step 3 — Review the Password Audit Result

The audit completed successfully and recovered the following password:

```text
harrypotter
```

This is the result identified in the laboratory activity.

The exact username associated with the recovered password and the full terminal output are not included in the activity summary provided for this documentation.

The recovered value is preserved here because it was explicitly identified in the practical result.

### Step 4 — Understand the Wordlist Result

A successful wordlist match demonstrates that the recovered password was present among the tested candidates or was otherwise recognized by the selected password auditing configuration.

The result indicates that the password could be recovered using the supplied wordlist and the selected hash format.

The activity does not require inventing additional account records or hash values to document the result.

## 5. Expected Results

The expected result is successful password recovery from the supplied `unshadow.txt` input.

| Item | Result |
|---|---|
| Input File | `unshadow.txt` |
| Hash Format | `crypt` |
| Attack Mode | Wordlist |
| Wordlist | `/usr/share/john/password.lst` |
| Recovered Password | `harrypotter` |

The recovered password demonstrates the importance of identifying weak passwords during a security assessment or forensic investigation.

## 6. Technical Analysis

### Why Use a Wordlist?

Wordlist attacks test candidate passwords from a predefined collection.

They can be effective when users choose common words, names, predictable strings, or other passwords included in the list.

The success of this method depends on factors such as:

- Password complexity.
- Wordlist contents.
- Password hash algorithm.
- Hash configuration.
- Available computational resources.

In this activity, the supplied wordlist was sufficient to recover the password `harrypotter`.

### The `--format=crypt` Option

John supports multiple password formats.

The `--format` option selects the implementation used to interpret the supplied password hashes.

The activity explicitly uses:

```bash
--format=crypt
```

This is important because the tool must interpret the input using a compatible hash format.

### The `--wordlist` Option

The option:

```bash
--wordlist=/usr/share/john/password.lst
```

selects a candidate password file.

John processes the candidate entries and tests them against the supplied hashes.

The use of a wordlist differs from brute-force searching, in which candidate combinations are generated according to a defined character set and length.

### Password Recovery and Forensic Significance

A recovered password may help an examiner understand the security condition of an account or identify the use of weak credentials.

However, password recovery alone does not establish who used an account or whether a particular user performed an action.

The result must be interpreted alongside other evidence, including timestamps, authentication logs, account records, and system activity.

### Evidence Protection

Recovered passwords and password hashes are sensitive information.

They should be kept within the authorized forensic environment and should not be published unnecessarily.

The portfolio documentation records the result required by the course without reproducing unrelated credential material.

## 7. Results and Interpretation

The activity demonstrates password auditing using John the Ripper.

The supplied `unshadow.txt` file was processed with the `crypt` format and the wordlist:

```text
/usr/share/john/password.lst
```

The recovered password was:

```text
harrypotter
```

The result shows that wordlist-based password auditing can identify weak credentials in recovered Unix authentication data.

The exercise also demonstrates the importance of password strength and the need to protect credential databases during incident response and forensic investigations.

## 8. Concepts Practiced

- Unix password storage
- `/etc/passwd`
- `/etc/shadow`
- Unshadow format
- John the Ripper
- Password hash formats
- `crypt`
- Wordlist attacks
- Candidate password testing
- Password auditing
- Credential forensics
- Sensitive evidence handling

## 9. Evidence

**Required screenshot: Print 3 — PDF page 3.**

The screenshot should show the John the Ripper command and the resulting password recovery.

The required result is:

```text
harrypotter
```

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 11.3 is on page 3 of the consolidated PDF.

## References

- [John the Ripper — Official Documentation](https://www.openwall.com/john/doc/)
- [John the Ripper — Wordlist Mode](https://www.openwall.com/john/doc/MODES.shtml)
- [John the Ripper — Command-Line Options](https://www.openwall.com/john/doc/OPTIONS.shtml)

---

[Back to Class 01](../README.md) · [Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
