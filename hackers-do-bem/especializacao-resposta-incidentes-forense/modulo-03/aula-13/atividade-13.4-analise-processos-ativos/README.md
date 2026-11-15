# Activity 13.4 — Active Process Analysis in Memory

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 13  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Examine process information preserved in a Windows memory image using Volatility 3.

The activity investigates active process artifacts and their relationships, including process identifiers and parent-child relationships.

Process analysis is important during incident response because malicious activity can be associated with an unusual process, an unexpected parent-child relationship, or an executable that does not match the expected system behavior.

The exercise uses the Windows memory image:

```text
memoria.img
```

The objective is to identify process information and understand how a process listing or process tree can support forensic reconstruction.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux forensic workstation |
| Forensic Framework | Volatility 3 |
| Framework Version Identified | 2.7.0 |
| Memory Image | `memoria.img` |
| Memory Image Location | `/home/aluno/coleta/memoria.img` |
| Target Operating System | Windows XP SP2 |
| Target Architecture | 32-bit |
| Main Plugins | `windows.pslist` and `windows.pstree` |
| Additional Process Artifact Plugin | `windows.cmdline` |

The target operating system was identified in Activity 13.3 using `windows.info`.

## 3. Process Forensics Concepts

### Processes in Memory

A process is an executing instance of a program.

A Windows process has a process identifier (PID), and may contain threads, handles, loaded modules, and memory regions.

A memory image can preserve information about processes that were active at the time of acquisition.

This information can support investigations involving suspicious programs, unauthorized execution, and process relationships.

### PID and PPID

The process identifier (PID) identifies a process.

The parent process identifier (PPID) identifies the process that created or launched another process.

Examining both values helps reconstruct process relationships.

For example, an unexpected command interpreter launched by an unusual parent process may warrant further investigation.

### windows.pslist

The `windows.pslist` plugin lists process structures identified in the Windows memory image.

It provides information such as:

- PID.
- Parent process ID.
- Process name.
- Process memory offset.
- Thread count.
- Handle count.
- Session information.
- Creation time.
- Exit time, when available.

The plugin provides a structured process listing.

### windows.pstree

The `windows.pstree` plugin presents processes in a parent-child hierarchy.

This makes it easier to visualize which processes created other processes.

The tree can help identify unusual execution relationships and suspicious process chains.

### windows.cmdline

The `windows.cmdline` plugin retrieves command-line information associated with processes when that information is available in memory.

Command-line information may provide additional context about the executable or parameters used to launch a process.

It complements the process list but does not replace it.

## 4. Procedure

### Step 1 — Access the Memory Analysis Working Directory

The Linux forensic workstation was used to analyze the Windows memory image.

The working directory used in the previous activity was:

```bash
cd /home/aluno/coleta
```

The memory image is:

```text
memoria.img
```

The system information previously obtained using `windows.info` identifies the image as Windows XP SP2, 32-bit.

This information is important because the available plugin support depends on the target operating system version and architecture.

### Step 2 — List Processes with windows.pslist

The process list can be generated using:

```bash
volatility -f memoria.img windows.pslist
```

The command components are:

| Component | Function |
|---|---|
| `volatility` | Starts Volatility 3 |
| `-f memoria.img` | Specifies the memory image |
| `windows.pslist` | Lists process structures from the Windows image |

The plugin produces a structured table of process information.

The table can include fields such as:

| Field | Description |
|---|---|
| PID | Process identifier |
| PPID | Parent process identifier |
| ImageFileName | Process executable name |
| Offset | Process object offset |
| Threads | Number of associated threads |
| Handles | Number of open handles |
| SessionId | Session identifier |
| Wow64 | Indicates WOW64 process information when applicable |
| CreateTime | Process creation time |
| ExitTime | Process exit time, when available |

The exact process rows and values are specific to `memoria.img` and must be taken from the original terminal output.

### Step 3 — Examine the Process Hierarchy

A process tree can be generated with:

```bash
volatility -f memoria.img windows.pstree
```

The `windows.pstree` plugin organizes process information according to parent-child relationships.

This view helps identify the process hierarchy and understand how individual processes were started.

The output should be examined for:

- Parent process identifiers.
- Child process identifiers.
- Process names.
- Unexpected parent-child relationships.
- Processes that appear outside the expected execution hierarchy.

The exact process tree from the laboratory is not included in the activity notes available for this documentation.

The required evidence should therefore be transcribed from the original terminal screenshot rather than replaced with a sample process tree.

### Step 4 — Correlate Process Names with Command-Line Information

The process list can be complemented with command-line information:

```bash
volatility -f memoria.img windows.cmdline
```

The plugin examines command-line information associated with processes.

This may provide the path or arguments used when a process was launched.

The output can help distinguish processes with similar executable names or identify an unexpected command line.

The screenshot description supplied for this activity refers to process identifiers and executable paths. The original screenshot should be used to identify the exact fields and plugin output shown in the laboratory.

## 5. Expected Results

The activity demonstrates the extraction of process information from the Windows memory image.

The process analysis can provide:

| Information | Forensic Purpose |
|---|---|
| PID | Identifies each process |
| PPID | Establishes parent-child relationships |
| ImageFileName | Identifies the process name |
| CreateTime | Provides temporal context |
| ExitTime | Indicates whether a process has terminated, when available |
| Command line | Provides launch parameters and possible executable path information |
| Process tree | Visualizes process execution relationships |

The process list and hierarchy provide a foundation for identifying unusual activity.

## 6. Technical Analysis

### Process Listing Versus Process Tree

The process list and process tree provide different representations of the same general class of artifact.

| Plugin | View |
|---|---|
| `windows.pslist` | Structured process listing |
| `windows.pstree` | Parent-child process hierarchy |
| `windows.cmdline` | Command-line information |

The process list is useful when examining individual PIDs, names, and timestamps.

The process tree is useful when investigating how processes relate to each other.

The command-line plugin provides context about how a process was started.

### PID and Parent-Child Relationships

A process tree can reveal relationships that are less obvious in a flat table.

An unexpected relationship may indicate suspicious execution or a process launched by an unusual parent.

However, process names and parent-child relationships should not be treated as proof of malicious activity by themselves.

They must be correlated with timestamps, command-line information, loaded modules, file artifacts, and network activity.

### Process Creation and Termination Times

Creation and termination timestamps can help establish the sequence of execution.

A process with a creation time near another suspicious event may warrant additional investigation.

The values should be interpreted using the timestamp and timezone context of the memory image.

### Command-Line Correlation

The `windows.cmdline` plugin can provide arguments and command-line details associated with a process.

This can help identify the executable path or parameters used to launch it.

The command line should be compared with the process name and memory artifacts.

### Limitations of Process Enumeration

A standard process list may not reveal every process artifact.

Some processes may have terminated or may no longer be linked into the normal process list.

Other Volatility plugins, such as `windows.psscan`, can scan memory for process structures independently.

This activity focuses on the process listing and hierarchy described by the practical exercise.

## 7. Results and Interpretation

The activity demonstrates how Volatility 3 can extract process information from the Windows memory image.

The process listing provides identifiers, process names, and execution-related information.

The process tree adds parent-child relationships, while command-line analysis can provide further details about executable invocation.

Together, these artifacts help reconstruct the execution state represented in the memory image.

The process results should be correlated with user environment variables and file paths found in Activity 13.3, as well as network artifacts examined in Activity 13.5.

## 8. Concepts Practiced

- Windows process forensics
- Memory image analysis
- Volatility 3
- `windows.pslist`
- `windows.pstree`
- `windows.cmdline`
- Process identifiers
- PID
- PPID
- Parent-child process relationships
- Process hierarchy
- Process creation time
- Process termination time
- Command-line analysis
- Executable identification
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 4 — PDF page 4 — Step 3.**

The screenshot should show the process listing or process tree obtained from the Windows memory image.

The evidence description requires the process identifiers and executable information to be visible.

The exact process names, PIDs, PPIDs, and command-line values should be taken from the original output.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 13.4 is on page 4 of the consolidated PDF.

## References

- [Volatility 3 — Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
- [Volatility 3 — Windows PsList](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.pslist.html)
- [Volatility 3 — Windows PsTree](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.pstree.html)
- [Volatility 3 — Windows CmdLine](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.cmdline.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 13.5](../atividade-13.5-artefatos-rede-memoria/README.md)
