# Activity 12.2 — Windows User Directory Investigation

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 02  
> **Course Lesson:** 12  
> **Environment:** forenseWin VM  
> **Status:** Completed

## 1. Objective

Examine extracted Windows user directories and the Recycle Bin to identify recovered artifacts associated with the group Anonymous.

The activity uses a logical copy of a Windows system partition supplied by the course.

The investigation focuses on the following locations:

```text
C:\C\Users
C:\C\$Recycle.Bin
```

The Recycle Bin is examined because deleted files may remain available as forensic artifacts.

The objective is to identify user-specific SID directories, inspect the files stored under those directories, and examine the contents of the recovered file `$ITYQLF6.txt`.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseWin` |
| Operating System | Windows |
| VM Address | `192.168.98.30` |
| Access Method | Remote workstation |
| Shell | Windows Command Prompt |
| Source Directory | `C:\curso\aula12` |
| Recovered Partition | `C` |
| Working Copy | `C:\C` |
| Recycle Bin Directory | `C:\C\$Recycle.Bin` |
| Investigated User SID | `S-1-5-21-761144124-354281791-3019405962-1000` |
| Relevant Artifact | `$ITYQLF6.txt` |

The course provides an extracted logical copy of a Windows partition. The data is examined from the forensic workstation rather than from the original seized disk.

## 3. Windows User Directories and Recycle Bin Concepts

### Windows User Directories

Windows stores user profile data under:

```text
C:\Users
```

A profile directory can contain user-specific files, application data, configuration information, and other artifacts.

During a forensic investigation, user profile directories are important locations to examine because they can contain evidence of account activity.

### Windows Security Identifiers

A Security Identifier (SID) uniquely identifies a security principal in Windows.

User-specific directories under the Recycle Bin are organized by SID.

The SID helps associate a deleted-file artifact with the Windows account that owned the corresponding Recycle Bin directory.

The exercise identifies two SID directories in the recovered partition.

### Windows Recycle Bin

The Recycle Bin stores deleted-file artifacts.

In modern Windows systems, the Recycle Bin uses files with `$I` and `$R` prefixes:

| Prefix | General Purpose |
|---|---|
| `$I` | Metadata associated with a deleted file |
| `$R` | Data of the deleted file |

The files are organized under the SID associated with the user.

The activity examines the recovered directory and reads the contents of the file identified by the course as `$ITYQLF6.txt`.

The exact role of this file should be interpreted from the recovered content and surrounding artifacts rather than assumed solely from its name.

### Windows Command Prompt

The `dir` command lists directory contents.

The `/a` option includes files and directories with hidden or system attributes.

The `type` command displays the contents of a text file.

These commands are used to inspect the logical partition and the relevant Recycle Bin artifact.

## 4. Procedure

### Step 1 — Examine the Recovered Windows Partition

The recovered partition was supplied under:

```text
C:\curso\aula12\C
```

The initial examination focused on the directory structure and user profiles.

The course material identifies the following user directories:

```text
Users
├── Public
└── Anom
```

The `Public` directory is a standard Windows profile directory, while `Anom` represents the additional user profile of interest in the case study.

The directory structure also suggested the presence of deleted-file artifacts in the Recycle Bin.

### Step 2 — Copy the Recovered Partition to the Working Location

The course instructions specify copying the recovered partition directory:

```text
C:\curso\aula12\C
```

to:

```text
C:\C
```

This creates a working copy for the command-line examination.

The Windows Command Prompt was then opened.

The following command was executed:

```cmd
cd C:\C
```

The current directory was inspected:

```cmd
dir
```

The course material provides the following output:

```text
C:\C> dir

 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

 Directory of C:\C

06/12/2023  03:01 AM    <DIR>          .
06/12/2023  03:01 AM    <DIR>          ..
06/12/2023  03:01 AM    <DIR>          $Recycle.Bin
06/12/2023  03:01 AM    <DIR>          Users

               0 File(s)              0 bytes
               7 Dir(s)  116,365,692,928 bytes free
```

The output shows two main directories relevant to the examination:

```text
$Recycle.Bin
Users
```

### Step 3 — Inspect the Recycle Bin

The Recycle Bin directory was accessed:

```cmd
cd Recycle.Bin
```

The directory contents were listed:

```cmd
dir
```

The output supplied in the course material is:

```text
C:\C\Recycle.Bin> dir

 Directory of C:\C\Recycle.Bin

 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

06/12/2023  03:01 AM    <DIR>          .
06/12/2023  03:01 AM    <DIR>          ..
06/12/2023  03:01 AM    <DIR>          S-1-5-21-2860833119-3973402386-1935623544-500
06/12/2023  03:01 AM    <DIR>          S-1-5-21-761144124-354281791-3019405962-1000

               0 File(s)              0 bytes
               4 Dir(s)  116,365,692,928 bytes free
```

The directories correspond to separate Windows user SIDs.

The activity focuses on the second SID:

```text
S-1-5-21-761144124-354281791-3019405962-1000
```

### Step 4 — Inspect the Second SID Directory

The contents of the second SID directory were examined:

```cmd
dir S-1-5-21-761144124-354281791-3019405962-1000
```

The course material provides the following output:

```text
C:\C\Recycle.Bin> dir S-1-5-21-761144124-354281791-3019405962-1000

 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

06/12/2023  03:01 AM    <DIR>          .
06/12/2023  03:01 AM    <DIR>          ..
06/12/2023  12:05 AM               325 $ITYQLF6.txt
06/12/2023  12:16 AM               127 desktop.ini

               2 File(s)            452 bytes
               2 Dir(s)  116,365,582,336 bytes free
```

Two files were identified:

| File | Size | Observation |
|---|---:|---|
| `$ITYQLF6.txt` | 325 bytes | File selected for content examination |
| `desktop.ini` | 127 bytes | Windows directory configuration file |

The file `$ITYQLF6.txt` was considered relevant because its name and location distinguished it from the ordinary configuration file.

The assignment requires a screenshot of this directory listing as part of the investigation.

### Step 5 — Examine the Recovered Text File

The second SID directory was entered:

```cmd
cd S-1-5-21-761144124-354281791-3019405962-1000
```

The file was displayed with:

```cmd
type $ITYQLF6.txt
```

The recovered text contained the following message:

```text
MESSAGE FROM #ANONYMOUS RABBIT:

"People shouldn't be afraid of their government, governments should
[remaining text truncated in the supplied course extraction]

The Central Bank of Russian Federation leak (28 GB) has been publish
[remaining text truncated in the supplied course extraction]

#Ukraine #OPRussia

pic.twitter.com/BJJBMpZESZ

- The Black Rabbit World (@Thblckrbbtworld) March 25, 2022
```

The file contains a message referencing Anonymous Rabbit and the hashtags:

```text
#Ukraine
#OPRussia
```

The material also references a purported leak involving the Central Bank of the Russian Federation.

The recovered text was considered an investigative lead connecting the recovered Windows data with the group referenced in the case study.

## 5. Expected Results

The activity identifies a suspicious text file within the Recycle Bin directory associated with the investigated SID.

The relevant artifacts are:

| Artifact | Finding |
|---|---|
| `C:\C\Users` | Contains the `Public` and `Anom` profile directories |
| `C:\C\$Recycle.Bin` | Contains user-specific SID directories |
| `S-1-5-21-761144124-354281791-3019405962-1000` | SID directory selected for examination |
| `$ITYQLF6.txt` | 325-byte file containing a message associated with Anonymous Rabbit |
| `desktop.ini` | Additional directory configuration artifact |

The recovered message provides a lead that can be correlated with other evidence.

## 6. Technical Analysis

### SID-Based Organization

The Recycle Bin uses SID-specific directories to separate deleted-file artifacts by user.

The directory:

```text
S-1-5-21-761144124-354281791-3019405962-1000
```

provides the security identifier associated with the recovered artifacts.

This allows the examiner to associate the directory with a particular Windows security principal when the corresponding account information is available.

### Recycle Bin Metadata and Deleted Data

The modern Recycle Bin stores metadata and deleted content in separate artifacts.

Generally:

- `$I` files preserve metadata about deleted items.
- `$R` files preserve the associated deleted content.

The file selected in this exercise was read directly with `type`.

Its actual contents provide the investigative value documented here.

The name alone is not sufficient to determine the complete role of a file. A forensic examiner should compare file structure, content, and related artifacts.

### Interpreting the Anonymous Message

The text recovered from `$ITYQLF6.txt` refers to Anonymous Rabbit and includes the hashtags `#Ukraine` and `#OPRussia`.

These references are relevant to the investigative scenario because the case study concerns possible connections with Anonymous.

However, the presence of a message in a deleted-file location does not independently prove that the account owner was a member of the group.

The artifact must be correlated with browser history, account activity, other recovered files, and additional evidence.

### Limitations of the Extracted Text

The text extraction supplied for this documentation is truncated in some sentences.

The complete text should be taken from the original recovered file or the evidence image.

Missing words should not be reconstructed from assumptions.

## 7. Results and Interpretation

The activity demonstrates how recovered Windows partition data can be examined to identify evidence in user directories and the Recycle Bin.

The investigation located two SID directories under `$Recycle.Bin`.

The second SID directory contained:

```text
$ITYQLF6.txt
desktop.ini
```

The recovered text file contained a message referencing Anonymous Rabbit, `#Ukraine`, and `#OPRussia`.

The artifact provides an investigative lead that can be correlated with the browser history and configuration artifacts examined in the following activities.

## 8. Concepts Practiced

- Windows forensics
- Logical partition examination
- Windows user profiles
- Windows Security Identifiers
- Recycle Bin analysis
- Deleted-file artifacts
- Hidden and system attributes
- Windows Command Prompt
- `dir`
- `dir /a`
- `type`
- Text artifact examination
- Evidence correlation
- Investigation of user activity

## 9. Evidence

**Required screenshot: Print 2 — PDF page 2 — Step 5.**

The assignment specifically requests the output of Step 5.

The screenshot should show:

- The Windows Command Prompt.
- The relevant SID directory.
- The command `type $ITYQLF6.txt`.
- The recovered message containing the Anonymous Rabbit references.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 12.2 is on page 2 of the consolidated PDF.

## References

- [Windows Forensics — Recycle Bin $I and $R Artifacts](https://github.com/libyal/dtformats/blob/main/documentation/Windows%20Recycle.Bin%20file%20formats.asciidoc)
- [Windows Forensic Artifacts — Recycle Bin Files](https://psmths.gitbook.io/windows-forensics/artifacts-by-type/filesystem-artifacts/recycle-bin-files)
- [Microsoft — Windows Command: dir](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/dir)
- [Microsoft — Windows Command: type](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/type)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 12.3](../atividade-12.3-arquivos-configuracao/README.md)
