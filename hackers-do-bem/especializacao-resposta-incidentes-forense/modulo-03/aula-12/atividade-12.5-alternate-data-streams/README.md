# Activity 12.5 — NTFS Alternate Data Streams Analysis

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 02  
> **Course Lesson:** 12  
> **Environment:** forenseWin VM  
> **Status:** Completed

## 1. Objective

Identify and examine an NTFS Alternate Data Stream (ADS) used to conceal data within another file.

The activity uses a Windows forensic workstation and the directory:

```text
C:\Slack
```

The supplied files include:

```text
pagamento.txt
wordpad.exe
WordpadFilter.dll
```

The exercise demonstrates how the contents of `pagamento.txt` can be redirected into a named data stream associated with `wordpad.exe`.

The activity then uses the `dir /r` command to identify the alternate stream and opens the stream using WordPad.

The objective is to understand how named NTFS data streams can conceal additional content from ordinary file browsing.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseWin` |
| Operating System | Windows |
| Filesystem | NTFS |
| Shell | Windows Command Prompt |
| Working Directory | `C:\Slack` |
| Cover File | `wordpad.exe` |
| Source Text File | `pagamento.txt` |
| Additional File | `WordpadFilter.dll` |
| Alternate Stream | `wordpad.exe:pagamento.txt:$DATA` |
| Detection Command | `dir /r` |
| Opening Command | `wordpad.exe wordpad.exe:pagamento.txt:$DATA` |

The course supplies the `Slack` directory under:

```text
C:\curso\aula12
```

The directory is copied to `C:\Slack` before the activity begins.

## 3. NTFS and Alternate Data Stream Concepts

### NTFS Streams

NTFS stores file data in streams.

A normal file has a default unnamed data stream.

NTFS also supports named alternate data streams, which allow additional content to be associated with an existing file.

The general syntax is:

```text
filename:streamname:streamtype
```

For example:

```text
wordpad.exe:pagamento.txt:$DATA
```

In this activity:

- `wordpad.exe` is the main file.
- `pagamento.txt` is the name of the alternate stream.
- `$DATA` identifies the data stream type.

### Alternate Data Streams

An Alternate Data Stream is a feature of NTFS that allows additional data to be associated with a file or directory.

The stream is separate from the file's default unnamed data stream.

A file can therefore contain additional data without that data appearing as an ordinary separate file in the directory listing.

This behavior can be abused to conceal information from basic file browsing and should be considered during forensic analysis.

### ADS Is Not the Same as File Slack

The course introduces ADS in a section discussing file spaces and slack spaces.

Technically, these are different concepts.

| Concept | Description |
|---|---|
| Alternate Data Stream | A named NTFS stream associated with a file |
| File slack | Unused space within the final allocated cluster of a file |
| Unallocated space | Disk clusters not currently allocated to a file |

ADS should therefore be treated as a separate NTFS stream mechanism rather than as file slack or unallocated disk space.

### The DIR /R Command

The Windows `dir` command supports the `/r` parameter to display alternate data streams.

A normal directory listing may show the main file without making its additional stream apparent.

The `/r` parameter exposes the stream name and associated size.

## 4. Procedure

### Step 1 — Copy and Inspect the Slack Directory

The course provides the working directory under:

```text
C:\curso\aula12\Slack
```

The directory was copied to:

```text
C:\Slack
```

The Windows Command Prompt was opened and the working directory was accessed:

```cmd
cd C:\Slack
```

The directory contents were listed:

```cmd
dir
```

The supplied output is:

```text
 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

 Directory of C:\Slack

06/15/2023  12:29 AM    <DIR>          .
06/15/2023  12:27 AM    <DIR>          en-US
06/14/2023  11:44 PM               956 pagamento.txt
06/15/2023  12:27 AM    <DIR>          pt-BR
05/16/2023  11:56 AM         3,006,464 wordpad.exe
11/20/2022  08:59 PM           204,800 WordpadFilter.dll

               3 File(s)      3,212,220 bytes
               3 Dir(s)  116,288,999,424 bytes free
```

The directory contains:

| Name | Size | Description |
|---|---:|---|
| `pagamento.txt` | 956 bytes | Text file used as the source of the hidden data |
| `wordpad.exe` | 3,006,464 bytes | Main file that will receive the alternate stream |
| `WordpadFilter.dll` | 204,800 bytes | Additional WordPad-related file |
| `en-US` | Directory | Application language resources |
| `pt-BR` | Directory | Application language resources |

The text file `pagamento.txt` is the source data for the alternate stream operation.

### Step 2 — Create an Alternate Data Stream

The command used to redirect the text file contents into the executable's alternate stream was:

```cmd
type pagamento.txt > wordpad.exe:pagamento.txt
```

The command components are:

| Component | Function |
|---|---|
| `type` | Reads and outputs the contents of a text file |
| `pagamento.txt` | Source text file |
| `>` | Redirects output |
| `wordpad.exe:pagamento.txt` | Named stream associated with `wordpad.exe` |

The redirection creates a named stream associated with `wordpad.exe`.

The alternate stream is named:

```text
pagamento.txt
```

The stream type is represented by NTFS as:

```text
$DATA
```

After creating the stream, the directory was listed again:

```cmd
dir
```

The supplied output is:

```text
 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

 Directory of C:\Slack

06/15/2023  12:29 AM    <DIR>          .
06/15/2023  12:27 AM    <DIR>          en-US
06/14/2023  11:44 PM               956 pagamento.txt
06/15/2023  12:27 AM    <DIR>          pt-BR
06/15/2023  12:33 AM         3,006,464 wordpad.exe
11/20/2022  08:59 PM           204,800 WordpadFilter.dll

               3 File(s)      3,212,220 bytes
               3 Dir(s)  116,288,831,488 bytes free
```

The ordinary file listing still shows `wordpad.exe` with a size of:

```text
3,006,464 bytes
```

The size of the main unnamed data stream is not changed in the ordinary directory listing.

The available disk space shown in the two supplied outputs changed from:

```text
116,288,999,424 bytes free
```

to:

```text
116,288,831,488 bytes free
```

The difference between those two reported values is 167,936 bytes.

This is the observed difference in the supplied directory outputs. It should not be interpreted as the exact size of the alternate stream itself.

### Step 3 — Detect the Alternate Data Stream

To identify the hidden stream, the activity used:

```cmd
dir /r
```

The `/r` parameter instructs Windows to display alternate data streams.

The supplied output contains the following entry:

```text
 Volume in drive C has no label.
 Volume Serial Number is FCBE-9131

 Directory of C:\Slack

06/15/2023  12:38 AM    <DIR>          .
06/15/2023  12:29 AM    <DIR>          en-US
06/14/2023  11:44 PM               956 pagamento.txt
06/15/2023  12:29 AM    <DIR>          pt-BR
06/15/2023  12:33 AM         3,006,464 wordpad.exe
                                     956 wordpad.exe:pagamento.txt:$DA...
11/20/2022  08:59 PM           204,800 WordpadFilter.dll

               3 File(s)      3,212,220 bytes
               3 Dir(s)  116,282,175,488 bytes free
```

The extracted course text clips the end of the stream type.

The complete NTFS stream name used in the next step is:

```text
wordpad.exe:pagamento.txt:$DATA
```

The output identifies an additional 956-byte stream associated with `wordpad.exe`.

This confirms that the content was stored as an alternate stream rather than as a separate ordinary file.

### Step 4 — Open the Alternate Stream

The final step opens the hidden stream using the associated application:

```cmd
wordpad.exe wordpad.exe:pagamento.txt:$DATA
```

The command components are:

| Component | Function |
|---|---|
| `wordpad.exe` | Starts the WordPad application |
| `wordpad.exe:pagamento.txt:$DATA` | Specifies the alternate data stream to open |

The command passes the alternate stream path to WordPad.

The application then opens the data associated with the named stream.

This demonstrates that the stream can be accessed even though its content does not appear as a separate ordinary file in the standard directory listing.

## 5. Expected Results

The activity demonstrates the creation, detection, and access of an NTFS Alternate Data Stream.

The relevant artifacts are:

| Item | Result |
|---|---|
| Main file | `wordpad.exe` |
| Source content | `pagamento.txt` |
| Named stream | `pagamento.txt` |
| Full stream path | `wordpad.exe:pagamento.txt:$DATA` |
| Stream size | 956 bytes |
| Detection command | `dir /r` |
| Opening command | `wordpad.exe wordpad.exe:pagamento.txt:$DATA` |

The activity demonstrates that the alternate stream can contain data associated with another file without appearing as a separate ordinary file in a normal directory listing.

## 6. Technical Analysis

### Stream Naming Syntax

NTFS uses a stream naming convention:

```text
filename:streamname:streamtype
```

The stream identified in this activity is:

```text
wordpad.exe:pagamento.txt:$DATA
```

The main file remains `wordpad.exe`.

The additional stream is named `pagamento.txt`, and its type is `$DATA`.

### Why the Ordinary DIR Output Did Not Show the Stream

The regular command:

```cmd
dir
```

lists the ordinary directory entries and main file sizes.

It does not enumerate the named alternate data stream in the same way as the `/r` option.

That is why `wordpad.exe` continues to appear with the main file size even after the alternate stream is created.

### Detecting ADS with DIR /R

The command:

```cmd
dir /r
```

is the key detection step in this exercise.

It displays alternate data streams associated with files in the current directory.

The output identifies the stream name and its size, allowing the analyst to locate files containing additional data.

This is particularly relevant during forensic examination because ADS content may not be visible through basic file browsing.

### ADS and File Size

The ordinary directory entry reports the size of the main unnamed stream.

Additional streams are stored separately and may not be reflected in that ordinary file-size display.

The course output shows that the main `wordpad.exe` size remained:

```text
3,006,464 bytes
```

The alternate stream was displayed separately as 956 bytes.

The available disk-space values also changed between the two directory listings.

The 167,936-byte difference is the difference between the two displayed free-space readings; it should not be treated as a direct measurement of the stream size.

### ADS Versus File Slack

Although the course presents this technique within a section discussing file spaces and slack spaces, ADS is not the same as file slack.

An Alternate Data Stream is a named NTFS stream that can store additional file content.

File slack refers to unused space in the final allocated cluster of a file.

Unallocated space refers to disk clusters that are not currently assigned to files.

These concepts may all be relevant in forensic analysis, but they describe different storage mechanisms.

### Forensic Significance

An attacker may use ADS to conceal additional information within an ordinary-looking file.

The main file can appear normal in a basic file listing, while the alternate stream stores separate content.

Forensic examinations should therefore enumerate streams, not rely exclusively on standard directory listings.

## 7. Results and Interpretation

The activity demonstrates how NTFS Alternate Data Streams can be used to associate hidden content with an existing file.

The source text file:

```text
pagamento.txt
```

was redirected to the alternate stream of:

```text
wordpad.exe
```

The stream was identified using:

```cmd
dir /r
```

The full stream path was:

```text
wordpad.exe:pagamento.txt:$DATA
```

The stream was then opened using:

```cmd
wordpad.exe wordpad.exe:pagamento.txt:$DATA
```

The activity demonstrates why the examination of NTFS files should include alternate stream enumeration.

The `dir /r` command provides a straightforward method to reveal named streams that are not apparent in an ordinary directory listing.

## 8. Concepts Practiced

- Windows filesystem forensics
- NTFS
- File streams
- Alternate Data Streams
- Named data streams
- `$DATA` stream type
- Command Prompt
- `type`
- Output redirection
- `dir`
- `dir /r`
- NTFS file size interpretation
- File slack versus ADS
- Concealed data detection
- Forensic artifact validation
- Evidence preservation

## 9. Evidence

**Required screenshot: Print 5 — PDF page 5 — Step 4.**

The assignment requires the screenshot for Step 4.

The screenshot should demonstrate:

- The Windows Command Prompt in the `C:\Slack` directory.
- The command:

```cmd
wordpad.exe wordpad.exe:pagamento.txt:$DATA
```

- The resulting opening of the content stored in the alternate stream.

The screenshot should allow the examiner to confirm that the data associated with the stream was accessed through the supplied application.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 12.5 is on page 5 of the consolidated PDF.

## References

- [Microsoft — NTFS Streams Specification](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-fscc/c54dec26-1551-4d3a-a0ea-4fa40f848eb3)
- [Microsoft — File Streams](https://learn.microsoft.com/en-us/windows/win32/fileio/file-streams)
- [Microsoft — DIR Command](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/dir)
- [Microsoft Sysinternals — Streams](https://learn.microsoft.com/en-us/sysinternals/downloads/streams)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
