# Activity 11.1 - Timeline Analysis with mactime

## Overview

This activity creates a chronological timeline of filesystem activity using mactime, a utility included in The Sleuth Kit.

The supplied body file `otavio.fls` contains filesystem metadata used to reconstruct file activity during May 2010.

## Objectives

- Generate a timeline from a Sleuth Kit body file.
- Inspect chronological file activity.
- Identify relevant events during May 2010.
- Preserve the timeline in a text file for further investigation.

## Environment

| Component | Description |
|---|---|
| Forensic Toolkit | The Sleuth Kit |
| Timeline Utility | mactime |
| Input File | `otavio.fls` |
| Output File | `otavio.timeline` |
| Investigation Period | May 2010 |

## Procedure

### 1. Generate the Timeline

Run the supplied mactime command:

```bash
mactime -b otavio.fls > otavio.timeline
```

The `-b` option identifies the input body file. The output redirection saves the resulting chronological timeline to `otavio.timeline`.

### 2. Inspect the Timeline

Display the generated timeline:

```bash
cat otavio.timeline
```

Review the dates, timestamps, activity types, file paths, and other metadata.

### 3. Investigate the Relevant Period

Examine the entries corresponding to May 2010.

The timeline can be used to organize filesystem activity chronologically and support the reconstruction of actions performed during the investigation period.

## Expected Result

The `otavio.timeline` file contains the chronological activity derived from `otavio.fls`, including the events associated with May 2010.

## Evidence

**Required screenshot: Print 1 - PDF page 1.**

The terminal screenshot must show:

- The personalized terminal prompt.
- The execution of `mactime -b otavio.fls > otavio.timeline`.
- The inspection of `otavio.timeline`.
- The chronological file activity associated with May 2010.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- mactime reads a body file and sorts its records by timestamp.
- The Sleuth Kit body-file format is produced by utilities such as `fls`, `ils`, and `mac-robber`.
- MACB activity labels represent modified, accessed, changed, and created timestamps where supported by the filesystem.
- The timeline is an investigative aid and should be correlated with other artifacts before drawing conclusions.

## References

- [The Sleuth Kit - Body File Format](https://wiki.sleuthkit.org/Body-file/)
- [The Sleuth Kit - mactime](https://github.com/sleuthkit/sleuthkit/wiki/mactime)

## Navigation

- [Class 01 - Aula 11](../README.md)
- [Module 03](../../README.md)
- [Next Activity - 11.2](../atividade-11.2-reconstrucao-fatos-autopsy/README.md)
