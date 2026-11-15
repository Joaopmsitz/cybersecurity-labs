# Activity 11.4 — ZIP Password Recovery with fcrackzip

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 01  
> **Course Lesson:** 11  
> **Environment:** Linux forensic environment  
> **Status:** Completed

## 1. Objective

Perform a controlled brute-force password recovery test against the course-provided encrypted ZIP archive using `fcrackzip`.

The activity uses the archive:

```text
radicals.zip
```

The command restricts the candidate character set to lowercase letters and the password length to five characters.

The recovered ZIP password was:

```text
anarc
```

The objective is to understand how password recovery tools test candidate combinations against encrypted archive data.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | Linux |
| Password Recovery Tool | fcrackzip |
| Input Archive | `radicals.zip` |
| Attack Mode | Brute force |
| Character Set | Lowercase letters |
| Password Length | 5 characters |
| Validation Method | `unzip` verification through `-u` |
| Recovered Password | `anarc` |

The exact source directory of `radicals.zip` is not included in the activity notes available for this documentation.

## 3. ZIP Password Recovery Concepts

### Encrypted ZIP Archives

ZIP archives can contain compressed files protected by a password.

When password protection is enabled, the archive requires an appropriate password to access its protected contents.

During a forensic investigation, a password-protected archive can prevent immediate access to potentially relevant evidence.

### Brute-Force Password Recovery

A brute-force method tests combinations generated from a defined character set.

The search space depends on:

- Character set size.
- Minimum password length.
- Maximum password length.
- Password structure.
- Search configuration.

In this activity, the search was restricted to lowercase letters and a length of five characters.

### fcrackzip

`fcrackzip` is a command-line utility for testing passwords against encrypted ZIP archives.

It supports brute-force and dictionary modes.

The activity uses brute-force mode with explicit character-set and length constraints.

## 4. Procedure

### Step 1 — Identify the ZIP Archive

The file supplied for the exercise was:

```text
radicals.zip
```

The archive is the input to the password recovery procedure.

The activity was performed against the course-provided file as part of the authorized laboratory investigation.

### Step 2 — Execute the Brute-Force Test

The following command was executed:

```bash
fcrackzip -b -c 'a' -l '5' -u radicals.zip
```

The command components are:

| Component | Function |
|---|---|
| `fcrackzip` | Starts the ZIP password recovery utility |
| `-b` | Enables brute-force mode |
| `-c 'a'` | Restricts the character set to lowercase letters |
| `-l '5'` | Sets the password length to exactly five characters |
| `-u` | Uses `unzip` to validate a candidate password |
| `radicals.zip` | Input encrypted ZIP archive |

The character-set identifier `a` represents lowercase letters from `a` to `z`.

The length parameter restricts the search to five-character candidates.

The `-u` option attempts to decompress the first file using a candidate password, helping filter out false positives.

### Step 3 — Review the Recovery Result

The brute-force test identified the password:

```text
anarc
```

The recovered password contains five lowercase characters, matching the search constraints configured in the command.

The standard success message produced by fcrackzip is:

```text
PASSWORD FOUND!!!!: pw == anarc
```

This is the password recovery result recorded for the activity.

### Step 4 — Interpret the Search Configuration

The command restricted the search space to a specific character set and length.

The configuration can be summarized as:

| Parameter | Selected Value |
|---|---|
| Mode | Brute force |
| Character set | `a` — lowercase letters |
| Length | 5 |
| Archive validation | Enabled with `-u` |
| Target | `radicals.zip` |

This controlled search configuration is important because the number of candidate combinations grows rapidly as the character set or password length increases.

## 5. Expected Results

The activity successfully recovered the password of the supplied encrypted archive.

| Item | Result |
|---|---|
| Archive | `radicals.zip` |
| Tool | `fcrackzip` |
| Search Mode | Brute force |
| Character Set | Lowercase letters |
| Password Length | 5 characters |
| Recovered Password | `anarc` |

The recovered password allows the course-provided archive to be accessed for subsequent examination.

## 6. Technical Analysis

### Character Set and Search Space

The `-c 'a'` parameter restricts the candidate alphabet to lowercase letters.

There are 26 lowercase English letters.

When a password is exactly five characters long, the theoretical search space is:

\[
26^5 = 11,881,376
\]

This represents all possible five-character combinations using lowercase English letters.

Restricting the search to a known character set and length reduces the search space compared with testing all possible characters and lengths.

### The `-l` Option

The command uses:

```bash
-l '5'
```

The fcrackzip length option accepts a minimum and optional maximum length.

When only one length is supplied, the search is restricted to that length.

In this activity, the candidate passwords are five characters long.

### The `-u` Option

The command uses:

```bash
-u
```

This option attempts to decompress the first file using a guessed password.

It helps reject false positives in situations where an apparent password match cannot correctly extract the archive contents.

### Brute Force Versus Dictionary Mode

Brute-force mode systematically generates combinations from a selected character set.

Dictionary mode instead tests entries from a supplied password list.

The activity uses brute-force mode because the command includes:

```bash
-b
```

The character set and password length are also explicitly restricted.

### Forensic Context

Password recovery can allow access to encrypted files that may contain relevant evidence.

However, successful password recovery does not establish the origin or authenticity of the archive contents.

The recovered archive should still be examined, preserved, and correlated with other evidence from the case.

## 7. Results and Interpretation

The activity demonstrates how `fcrackzip` can test candidate passwords against an encrypted ZIP archive.

The command:

```bash
fcrackzip -b -c 'a' -l '5' -u radicals.zip
```

restricts the search to five-character combinations of lowercase letters and validates candidate matches using `unzip`.

The recovered password was:

```text
anarc
```

The result demonstrates how search constraints influence brute-force password recovery and how an encrypted archive can be made available for subsequent forensic examination.

## 8. Concepts Practiced

- ZIP archive encryption
- Password recovery
- fcrackzip
- Brute-force search
- Character-set selection
- Password length constraints
- Candidate password generation
- Archive validation
- False-positive reduction
- Search-space calculation
- Forensic access to encrypted files
- Evidence preservation

## 9. Evidence

**Required screenshot: Print 4 — PDF page 4.**

The screenshot should show the fcrackzip command and the recovery result.

The required password is:

```text
anarc
```

The terminal output should demonstrate that the recovered password belongs to the `radicals.zip` archive.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 11.4 is on page 4 of the consolidated PDF.

## References

- [fcrackzip — Debian Manual](https://manpages.debian.org/unstable/fcrackzip/fcrackzip.1.en.html)
- [fcrackzip — Arch Linux Manual](https://man.archlinux.org/man/extra/fcrackzip/fcrackzip.1.en)

---

[Back to Class 01](../README.md) · [Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
