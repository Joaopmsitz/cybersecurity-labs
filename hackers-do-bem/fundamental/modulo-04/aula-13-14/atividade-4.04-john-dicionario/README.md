# Activity 4.04 — John the Ripper: Dictionary Attack

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 13–14  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use John the Ripper to perform an offline password audit in a controlled environment, using a password hash stored on the system and a dictionary-based attack.

The activity demonstrates how weak passwords can be recovered when an attacker obtains access to stored password hashes, without having to make authentication attempts directly against the original service.

**Laboratory scope:** All procedures were performed exclusively with an account created for the exercise.

## Environment

- **Operating system:** Kali Linux
- **Tools:** John the Ripper, OpenSSL
- **Test file:** `credencial.txt`
- **System file examined:** `/etc/shadow`
- **Hash format used in the laboratory:** `crypt`
- **Method:** Dictionary attack

## Procedure

### 1. Access the `/etc/shadow` File

Administrative access was obtained first:

```bash id="shv0qa"
sudo -i
```

The `/etc/shadow` file was then inspected:

```bash id="qz6fda"
cat /etc/shadow
```

The `/etc/shadow` file contains authentication-related information for local accounts, including password hashes and password-aging parameters.

The laboratory output contained entries for several system users.

For security reasons, the actual hashes from the environment are not reproduced in this README.

An entry has a structure similar to:

```text id="m07vdt"
username:<hash>:...
```

Access to this file must be restricted because obtaining password hashes can enable offline password-cracking attempts.

### 2. Create a Test User

A user account exclusively for the activity was created using `useradd` and OpenSSL:

```bash id="wjac55"
useradd -p $(openssl passwd -1 [senha-de-teste]) teste1
```

In the laboratory, the OpenSSL `-1` option was used to generate a hash in the MD5-crypt format, identified by the `$1$` prefix.

**Note:** `[senha-de-teste]` is a placeholder for the test password used in the laboratory, not a literal password to enter unchanged. The test password is not reproduced in this README.

After creation, the `teste1` account had a corresponding entry in `/etc/shadow`.

### 3. Identify the Test Account Entry

The file was inspected again:

```bash id="5nq4si"
cat /etc/shadow
```

The entry associated with the newly created user had a structure similar to:

```text id="z9m8fp"
teste1:<hash-do-laboratório>:...
```

The purpose of this step was to identify the line corresponding to the test account.

The hash was used as input for the offline password-auditing process.

### 4. Create the Credential File

The entry corresponding to the `teste1` user was copied into a separate file:

```text id="b4mz9g"
credencial.txt
```

This file contained the material required for John the Ripper to attempt to identify the password corresponding to the hash.

Separating the hash into its own file avoided working directly with `/etc/shadow` during the exercise.

The hash in this file was laboratory test data, not a production credential.

### 5. Run John the Ripper

After preparing the test file, the following command was executed:

```bash id="a8jh12"
john -format=crypt credencial.txt
```

John identified the hash and began attempting recovery using its rules and the default wordlist.

**Observed output:**

```text id="vvpq57"
Created directory: /root/.john
Using default input encoding: UTF-8
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Cost 1 (algorithm [1:descrypt 2:md5crypt 3:sunmd5 4:bcrypt 5:sha256crypt 6:sha512crypt]) is 2 for all loaded hashes
Cost 2 (algorithm specific iterations) is 1 for all loaded hashes
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
[senha recuperada no laboratório]          (teste1)
1g 0:00:00:00 DONE 2/3 (2024-04-25 18:54) 1.960g/s 8364p/s 8364c/s 8364C/s Alexis..bigred
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

The execution displayed:

```text id="a9vruw"
Loaded 1 password hash
```

This indicates that one password hash was loaded for analysis.

The default wordlist was also used:

```text id="z7qnmt"
/usr/share/john/password.lst
```

The result:

```text id="jrf6ta"
1g 0:00:00:00 DONE
```

indicates that one credential was recovered during the execution.

The recovered plaintext password is not reproduced in this README because it corresponds to the password used in the laboratory.

### 6. Interpret the Results

The result demonstrates the difference between online authentication attempts and offline password attacks.

In this exercise, John the Ripper did not need to submit attempts to a login page. Instead, it received a password hash and worked locally to find a candidate that matched the stored hash.

The process can be represented as follows:

```text id="hxm67k"
Test password
      |
      v
Password hash stored in /etc/shadow
      |
      v
Copy of the hash -> credencial.txt
      |
      v
John the Ripper
      |
      v
Wordlist and candidate-generation rules
      |
      v
Comparison against the hash
      |
      v
Recovered password
```

This illustrates why protecting `/etc/shadow` is important: obtaining password hashes can allow offline cracking attempts without generating login attempts against the original authentication service.

The success of a dictionary attack depends on factors such as password predictability, the hash algorithm, its computational cost, and the candidates available to the cracking tool.

### 7. Remove the Test File

After completing the exercise, the directory contents were checked:

```bash id="c3ffm5"
ls
```

The file created for the activity was removed:

```bash id="g7n8zp"
rm credencial.txt
```

This cleanup step prevented an unnecessary copy of the test hash from being left behind.

Removing `credencial.txt` does not automatically delete the test account or its entry in `/etc/shadow`. The documented cleanup specifically removed the temporary hash file.

## Commands Used

The following commands were used during the activity:

```bash id="xmyjhm"
sudo -i
cat /etc/shadow
useradd -p $(openssl passwd -1 [senha-de-teste]) teste1
cat /etc/shadow
john -format=crypt credencial.txt
ls
rm credencial.txt
```

The test hash was handled in a separate file, and the recovered password is intentionally omitted from the documentation.

## Concepts Practiced

### `/etc/shadow`

A Linux file used to store password hashes and information related to password aging.

Unlike plaintext password storage, Linux authentication can verify a password without storing the original password directly in this file.

Because password hashes can be targeted by offline cracking tools, access to `/etc/shadow` must be tightly restricted.

### Password Hash

A password hash is the output of a function used to represent a password without storing the original value directly.

However, hashes generated with older algorithms or derived from weak passwords can be vulnerable to offline cracking.

### MD5-crypt

The laboratory used the following OpenSSL option:

```bash id="vnns6g"
openssl passwd -1
```

The `-1` option generates hashes in the MD5-crypt format, identified by the `$1$` prefix.

MD5-crypt is considered a legacy password-hashing scheme and should not be used as a model for modern password storage. Modern systems should use purpose-built password-hashing algorithms with appropriate work factors, such as Argon2id, scrypt, or appropriately configured bcrypt.

### John the Ripper

John the Ripper is a password-auditing tool that tests candidate passwords against known hashes.

It can use different techniques, including:

- Wordlists.
- Password-transformation rules.
- Multiple hash formats.
- Candidate combinations.

### Dictionary Attack

A dictionary attack tests candidate passwords drawn from a list or generated using predefined rules.

It is particularly effective against weak or predictable passwords that appear in the candidate set.

### Offline Attack

In an offline attack, the attacker works with a copy of authentication material, such as password hashes, without having to submit each candidate to the original authentication service.

Offline attacks can avoid generating login-failure events on the original service, which makes protecting stored hashes and selecting strong passwords especially important.

## Results

The activity demonstrated how John the Ripper can be used to audit a credential from its hash in a controlled environment.

The following tasks were completed:

- Examined the purpose of `/etc/shadow`.
- Created an account specifically for the laboratory.
- Generated a test credential using OpenSSL.
- Separated the hash into `credencial.txt`.
- Identified the `crypt` hash format.
- Executed John the Ripper.
- Used the default wordlist.
- Recovered the test password.
- Removed the temporary file after completing the exercise.

The exercise reinforced the importance of modern password-hashing algorithms, strong password policies, and restricted access to files containing authentication material.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 13–14.

**Recorded screenshot:** Step 7 of the activity, as required by the laboratory instructions, showing John the Ripper's execution and recovery of the test credential.

[View Evidence — Classes 13–14](../evidencias.pdf)

---

[Back to Classes 13–14](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
