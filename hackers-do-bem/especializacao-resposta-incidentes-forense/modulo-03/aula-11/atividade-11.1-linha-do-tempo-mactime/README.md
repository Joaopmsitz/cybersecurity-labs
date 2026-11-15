# Activity 11.1 — Filesystem Timeline Analysis with mactime

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 01  
> **Course Lesson:** 11  
> **Environment:** Linux forensic environment  
> **Status:** Completed

## 1. Objective

Generate and examine a chronological filesystem activity timeline using `mactime` from The Sleuth Kit.

The activity uses the supplied body file `otavio.fls` as the source of filesystem metadata and generates a timeline named `otavio.timeline`.

The objective is to reconstruct file activity from the timestamps recorded in filesystem metadata and identify events that occurred during May 2010.

Timeline analysis is an important forensic technique because it allows an investigator to organize file-related events chronologically and correlate them with other evidence.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | Linux |
| Forensic Framework | The Sleuth Kit |
| Timeline Utility | `mactime` |
| Input Body File | `otavio.fls` |
| Output Timeline | `otavio.timeline` |
| Main Operation | Filesystem timeline generation |
| Period of Interest | May 2010 |
| Output Format | ASCII text timeline |

The activity uses the body file supplied by the training environment. The exact source image and original path of `otavio.fls` are not included in the activity information available for this documentation.

## 3. Timeline Forensics Concepts

### Filesystem Metadata

A filesystem stores metadata associated with files and directories.

Depending on the filesystem, this metadata can include:

- File name and path.
- Inode or metadata identifier.
- File size.
- User and group identifiers.
- File permissions.
- Modification timestamps.
- Access timestamps.
- Metadata change timestamps.
- Creation or birth timestamps, when supported.

These records provide information that can help reconstruct activity on a system.

### The Sleuth Kit Body File

The Sleuth Kit uses a body-file format as an intermediate representation of filesystem metadata.

A body file contains records that can be processed by `mactime` to generate a chronological timeline.

The activity uses:

```text
otavio.fls
```

The file is the input to the timeline generation process.

### mactime

`mactime` reads body-file records and sorts filesystem activity according to their timestamps.

The utility can display file activity as an ASCII timeline.

The `-b` option specifies the body file that will be processed.

The generated timeline can help identify periods of activity, changes to files, and events that may require further investigation.

### MACB Timestamps

Timeline analysis commonly uses four timestamp categories:

| Letter | Timestamp | Description |
|---|---|---|
| M | Modified | Time when file content was modified |
| A | Accessed | Time when the file was accessed |
| C | Changed | Time when filesystem metadata was changed |
| B | Created / Birth | File creation time, when supported by the filesystem |

The actual availability and interpretation of these timestamps depend on the filesystem and the metadata collected.

## 4. Procedure

### Step 1 — Identify the Supplied Body File

The activity uses the previously supplied body file:

```text
otavio.fls
```

The body file contains filesystem metadata records that will be processed by `mactime`.

It is important to distinguish the body file from the resulting timeline:

| File | Purpose |
|---|---|
| `otavio.fls` | Input containing filesystem metadata |
| `otavio.timeline` | Chronologically sorted timeline generated from the input |

### Step 2 — Generate the Timeline

The timeline was generated using:

```bash
mactime -b otavio.fls > otavio.timeline
```

The command components are:

| Component | Function |
|---|---|
| `mactime` | Executes the timeline analysis utility |
| `-b` | Specifies the input body file |
| `otavio.fls` | Body file containing filesystem metadata |
| `>` | Redirects standard output to a file |
| `otavio.timeline` | Destination file for the generated timeline |

The command reads the records from `otavio.fls`, organizes the activity chronologically, and redirects the resulting text to `otavio.timeline`.

Because the output is redirected, the timeline is saved to the file instead of being printed directly to the terminal.

### Step 3 — Inspect the Generated Timeline

After generation, the resulting file was inspected:

```bash
cat otavio.timeline
```

The `cat` command displays the contents of the timeline file in the terminal.

The output contains filesystem activity organized chronologically.

The timeline can include fields such as:

| Field | Description |
|---|---|
| Date/Time | Date and time associated with the event |
| Size | File size in bytes |
| Activity Type | Timestamp category associated with the event |
| Permissions | Recorded file permissions |
| User ID | User identifier associated with the file |
| Group ID | Group identifier associated with the file |
| Inode | Filesystem metadata identifier |
| File Name | Path or name of the associated file |

The exact event rows are dependent on the supplied `otavio.fls` file. They should be read from the original timeline output rather than replaced with invented records.

### Step 4 — Examine the May 2010 Activity

The generated timeline was examined to identify chronological filesystem activity from May 2010.

The investigation focused on the dates and timestamps associated with the records.

The timeline provides a chronological view that helps the analyst identify when files were modified, accessed, or had metadata changes recorded.

The activity requires examining the events from May 2010 and interpreting their order.

The specific file paths and individual timestamps are not reproduced here because they were not included in the activity description supplied for this documentation.

## 5. Expected Results

The command:

```bash
mactime -b otavio.fls > otavio.timeline
```

generates the file:

```text
otavio.timeline
```

The expected result is a chronological text representation of filesystem activity based on the metadata contained in `otavio.fls`.

The investigation focuses on activity recorded during May 2010.

The timeline provides the basis for identifying relevant file events and reconstructing the sequence of activity.

## 6. Technical Analysis

### Why Generate a Timeline?

A filesystem contains metadata associated with file operations.

Examining individual timestamps separately can make it difficult to understand the sequence of activity.

Timeline generation places these records in chronological order, allowing an examiner to identify relationships between events.

For example, a sequence of file creation, modification, and access records may help establish how a particular artifact was used.

### The Role of the Body File

The body file acts as an intermediate source between filesystem metadata collection and timeline generation.

`mactime` does not directly create the body file. It reads the body-file records and organizes them chronologically.

The Sleuth Kit's `fls` utility can generate body-file output using its timeline-related options.

The input `otavio.fls` was already available for this activity, so the procedure focused on generating and inspecting the timeline.

### Output Redirection

The command uses the shell redirection operator:

```bash
>
```

This directs the standard output of `mactime` into `otavio.timeline`.

Without redirection, the timeline would be printed to the terminal. With redirection, the result is preserved as a separate file that can be inspected later.

### Interpreting Timeline Events

The timeline should be analyzed in context.

A timestamp alone does not establish malicious activity. It must be correlated with other records, such as application logs, operating system events, user activity, and other forensic artifacts.

The May 2010 records provide a chronological starting point for examining the activity contained in the supplied forensic dataset.

## 7. Results and Interpretation

The activity demonstrates how The Sleuth Kit's `mactime` utility can transform a filesystem body file into a chronological timeline.

The supplied `otavio.fls` file was processed using:

```bash
mactime -b otavio.fls > otavio.timeline
```

The resulting file was then inspected to examine filesystem activity from May 2010.

This procedure provides a foundation for reconstructing file activity and identifying events that may be relevant to a digital forensic investigation.

## 8. Concepts Practiced

- Digital forensics
- Filesystem metadata
- The Sleuth Kit
- Body-file format
- `mactime`
- Timeline generation
- MACB timestamps
- Chronological event analysis
- Output redirection
- Filesystem activity reconstruction
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 1 — PDF page 1.**

The consolidated evidence must show the timeline generation command and the resulting timeline.

The screenshot should demonstrate:

- The command `mactime -b otavio.fls > otavio.timeline`.
- The generated file `otavio.timeline`.
- The chronological filesystem activity.
- The relevant records from May 2010.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 11.1 is on page 1 of the consolidated PDF.

## References

- [The Sleuth Kit — mactime](https://github.com/sleuthkit/sleuthkit/wiki/mactime)
- [The Sleuth Kit — Body File Format](https://wiki.sleuthkit.org/Body-file/)
- [The Sleuth Kit — Mactime Output](https://wiki.sleuthkit.org/Mactime-output/)
- [The Sleuth Kit — Timeline Analysis](https://github.com/sleuthkit/sleuthkit/wiki/Timelines)

---

[Back to Class 01](../README.md) · [Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
