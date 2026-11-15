# Activity 10.1 — Linux Memory Dump with AVML

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 02  
> **Class:** 10  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Acquire a snapshot of volatile memory from the `forenseLinux` virtual machine using AVML (Acquire Volatile Memory for Linux).

The exercise demonstrates the acquisition of physical memory from a running Linux system and the preparation of the resulting forensic artifact for subsequent analysis.

Volatile memory can contain information that is not necessarily preserved on disk, such as running processes, active network connections, loaded modules, command execution context, and other runtime data.

The acquisition process uses the AVML binary supplied by the course to generate a memory image named `memoria.dump`.

After acquisition, MD5 and SHA-256 hashes are generated to provide cryptographic identifiers that can be used to verify the integrity of the collected image.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux |
| User Account | `aluno` |
| Privilege Level | Root |
| Memory Acquisition Tool | AVML |
| Source Directory | `/curso/aula10` |
| Working Directory | `/home/aluno/forense` |
| Acquisition Binary | `avml` |
| Output Image | `memoria.dump` |
| MD5 File | `memoria.dump.md5` |
| SHA-256 File | `memoria.dump.sha256` |
| Hash Utilities | `md5sum` and `sha256sum` |

## 3. Memory Forensics and Acquisition Concepts

### Volatile Memory

Volatile memory is temporary data stored in RAM while the operating system is running.

Unlike files stored on persistent storage, RAM contents may disappear when the machine is shut down or restarted.

Memory acquisition is therefore important when an investigation requires information about the system's runtime state.

A memory image can later be examined to investigate processes, loaded modules, network activity, credentials in memory, and other artifacts, depending on the data available and the forensic tools used.

### AVML — Acquire Volatile Memory for Linux

AVML is a memory acquisition utility developed by Microsoft for Linux systems.

The laboratory provides an AVML executable in:

```bash
/curso/aula10
```

The activity uses the supplied binary directly from the working directory:

```bash
./avml memoria.dump
```

The command specifies the output filename for the acquired memory image.

### Cryptographic Hashes

Cryptographic hashes provide fixed-length values calculated from file contents.

This activity generates two hashes:

| Algorithm | Command | Purpose |
|---|---|---|
| MD5 | `md5sum` | Generate an MD5 digest of the memory image |
| SHA-256 | `sha256sum` | Generate a SHA-256 digest of the memory image |

The generated values can be recalculated later and compared with the original values to check whether the acquired file has changed.

Hashing does not encrypt the memory image. It provides a way to identify changes in file contents.

## 4. Procedure

### Step 1 — Obtain Root Privileges

The first step was to open a root shell to obtain the permissions required for memory acquisition and file management.

The following command was executed:

```bash
sudo su
```

This command starts a shell with root privileges.

After successful authentication, the terminal changes to the root shell. The exact prompt depends on the Linux configuration.

### Step 2 — Create the Forensic Working Directory

A dedicated directory was created to store the AVML binary, memory image, and hash files.

The directory was created using:

```bash
mkdir /home/aluno/forense
```

The terminal then entered the newly created directory:

```bash
cd /home/aluno/forense
```

The supplied AVML executable was copied from the course directory:

```bash
cp /curso/aula10/avml .
```

The destination `.` represents the current working directory, so the binary was copied to:

```text
/home/aluno/forense/avml
```

These commands normally do not print confirmation messages when successful. The terminal returns to the command prompt.

The resulting directory structure at this stage is:

```text
/home/aluno/forense/
└── avml
```

This is the expected structure, not a verbatim copy of the terminal output.

### Step 3 — Grant Execution Permission to AVML

After copying the binary, execution permission was granted:

```bash
chmod a+x avml
```

The `chmod` command changes file permissions.

The `a+x` parameter adds execution permission for all user categories:

| Permission | Meaning |
|---|---|
| `a` | All users: owner, group, and others |
| `+` | Add the specified permission |
| `x` | Execute permission |

This operation allows the binary to be invoked directly from the terminal.

### Step 4 — Acquire Volatile Memory

With the binary prepared, the memory acquisition was performed using:

```bash
./avml memoria.dump
```

The command components are:

| Component | Function |
|---|---|
| `./` | Executes a file from the current directory |
| `avml` | AVML acquisition binary |
| `memoria.dump` | Name assigned to the resulting memory image |

The command instructs AVML to acquire volatile memory and write the resulting image to `memoria.dump` in the current working directory.

The expected output artifact is:

```text
/home/aluno/forense/memoria.dump
```

The exact progress messages and terminal output depend on the supplied binary and execution environment. The available activity notes do not include a literal AVML execution transcript.

### Step 5 — Inspect the Generated Files

After the acquisition, the working directory was inspected:

```bash
ls -la
```

The command lists directory contents.

The `-l` parameter displays detailed information, including file permissions, ownership, size, and modification time.

The `-a` parameter includes hidden entries.

After a successful acquisition, the directory should contain the AVML executable and the generated memory image:

```text
/home/aluno/forense/
├── avml
└── memoria.dump
```

The exact file sizes, permissions, timestamps, and ownership values depend on the laboratory environment and are not reproduced here because they were not included in the supplied activity transcript.

### Step 6 — Generate the MD5 Hash

The MD5 hash was generated and redirected to a separate file:

```bash
md5sum memoria.dump > /home/aluno/forense/memoria.dump.md5
```

The command calculates the MD5 digest of `memoria.dump`.

The `>` redirection operator writes the command output to:

```text
/home/aluno/forense/memoria.dump.md5
```

Because the output is redirected, the hash is saved to the file instead of being displayed directly in the terminal.

The generated file stores the hash value associated with the acquired memory image.

### Step 7 — Generate the SHA-256 Hash

The SHA-256 digest was generated using:

```bash
sha256sum memoria.dump > /home/aluno/forense/memoria.dump.sha256
```

This command calculates the SHA-256 digest of the same memory image.

The output is redirected to:

```text
/home/aluno/forense/memoria.dump.sha256
```

As with the MD5 command, the result is stored in a file rather than printed directly in the terminal.

### Step 8 — Inspect the Complete Working Directory

After generating both hashes, the working directory was inspected again:

```bash
ls -la
```

At this point, the expected directory structure is:

```text
/home/aluno/forense/
├── avml
├── memoria.dump
├── memoria.dump.md5
└── memoria.dump.sha256
```

The directory contains:

| File | Description |
|---|---|
| `avml` | Supplied memory acquisition executable |
| `memoria.dump` | Acquired volatile memory image |
| `memoria.dump.md5` | File containing the MD5 digest |
| `memoria.dump.sha256` | File containing the SHA-256 digest |

The activity material does not provide the literal output of this final listing or the actual hash values. They should be preserved from the original terminal evidence rather than replaced with estimated values.

### Step 9 — Clean Up the Laboratory Directory

The course instructions include removing the working directory after completing the activity.

First, return to the user's home directory:

```bash
cd /home/aluno
```

Then remove the forensic working directory:

```bash
rm -r forense/
```

The `rm -r` command recursively removes the directory and its contents.

This operation deletes the AVML binary, memory image, and generated hash files stored in the working directory.

**Important:** cleanup should only be performed after confirming that the acquired image, hash files, and any required evidence have been preserved. In a real forensic investigation, the original evidence should remain protected and available for subsequent examination.

## 5. Expected Results

The activity produces a memory image and two associated cryptographic hash files.

The expected directory contents after acquisition and hash generation are:

```text
avml
memoria.dump
memoria.dump.md5
memoria.dump.sha256
```

The resulting artifacts have the following purposes:

| Artifact | Purpose |
|---|---|
| `memoria.dump` | Stores the acquired volatile memory |
| `memoria.dump.md5` | Stores the MD5 digest of the memory image |
| `memoria.dump.sha256` | Stores the SHA-256 digest of the memory image |

The generated hashes can be used later to verify whether the contents of `memoria.dump` have remained unchanged.

## 6. Technical Analysis

### Memory Acquisition from a Running System

The activity performs memory acquisition while the Linux virtual machine is running.

This is important because volatile memory contains runtime information that may be lost when the operating system is powered off.

The acquired image provides a snapshot of memory at the time of collection. The image can be used as input for later memory forensic analysis.

### Execution Permissions

The command:

```bash
chmod a+x avml
```

adds executable permission to the supplied binary.

Linux does not necessarily permit a copied file to be executed directly. The permission change prepares the binary for invocation from the command line.

### AVML Command Syntax

The laboratory uses:

```bash
./avml memoria.dump
```

This syntax corresponds to the executable and command format supplied for the course exercise.

The current Microsoft AVML project also documents a subcommand-based interface, using commands such as:

```bash
avml acquire memoria.dump
```

The two forms should not be treated as interchangeable without checking the version of the executable being used.

The original laboratory command was retained in this documentation because it reflects the procedure supplied for the exercise.

### MD5 and SHA-256 Integrity Verification

The commands:

```bash
md5sum memoria.dump
sha256sum memoria.dump
```

calculate cryptographic digests from the memory image.

The activity redirects each result to a separate file:

```bash
md5sum memoria.dump > /home/aluno/forense/memoria.dump.md5
sha256sum memoria.dump > /home/aluno/forense/memoria.dump.sha256
```

The resulting hash files can be retained with the forensic image.

During later verification, the hash can be recalculated and compared with the recorded value. A mismatch indicates that the contents of the file are no longer identical to the contents used to generate the original digest.

SHA-256 is preferable to MD5 for modern integrity workflows because MD5 has known collision weaknesses. The activity nevertheless generates both because the training exercise explicitly requests them.

### Evidence Preservation and Cleanup

The working directory contains the original acquisition output and its associated hash records.

Deleting this directory before preserving the evidence would remove the acquired image and the hash files required for subsequent verification.

In a forensic workflow, evidence should be copied to an appropriate storage destination, protected from unauthorized modification, and documented before temporary laboratory files are removed.

## 7. Results and Interpretation

The activity demonstrates the acquisition of volatile memory from a Linux virtual machine using AVML.

The procedure begins by obtaining root privileges, preparing a dedicated working directory, and copying the supplied acquisition binary.

The executable is granted permission to run and used to create `memoria.dump`.

After acquisition, MD5 and SHA-256 hashes are generated and stored in separate files. This creates a basic integrity record associated with the memory image.

The final directory inspection provides an overview of the artifacts generated during the activity.

The exercise establishes a basic memory acquisition workflow that can be followed by subsequent forensic examination using appropriate memory analysis tools.

## 8. Concepts Practiced

- Linux privilege management
- Root shell access
- Linux directory management
- File copying and permissions
- Volatile memory acquisition
- AVML
- Memory forensic imaging
- MD5 hashing
- SHA-256 hashing
- Output redirection
- Evidence integrity verification
- Forensic evidence preservation
- Laboratory cleanup procedures

## 9. Evidence

**Required screenshot: Step 2 — Print 1, PDF page 1.**

The course instructions require a terminal screenshot showing the preparation of the forensic working directory.

The screenshot should contain:

- The personalized terminal prompt.
- The command used to create `/home/aluno/forense`.
- The command used to enter the working directory.
- The command copying AVML from `/curso/aula10`.
- The prepared working directory before memory acquisition.

The terminal prompt must be configured using the alias required by the course.

Execute the following command in the Linux terminal:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\\u/meunome/g')"
```

Replace `meunome` with the required student alias.

The assignment instructs students to execute this command again whenever a new Linux terminal session is opened.

[View Universal Class Evidence PDF](../evidences.pdf)

The PDF consolidates the screenshots submitted for the practical activities in Class 10.

## References

- [Microsoft — AVML: Acquire Volatile Memory for Linux](https://github.com/microsoft/avml)
- [Linux manual — chmod](https://man7.org/linux/man-pages/man1/chmod.1.html)
- [Linux manual — md5sum](https://man7.org/linux/man-pages/man1/md5sum.1.html)
- [Linux manual — sha256sum](https://man7.org/linux/man-pages/man1/sha256sum.1.html)
- [Linux manual — rm](https://man7.org/linux/man-pages/man1/rm.1.html)

---

[Back to Class 10](../README.md) · [Back to Module 02](../../README.md) · [Back to Specialization](../../../README.md)
