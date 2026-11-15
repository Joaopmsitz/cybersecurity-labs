# Activity 13.3 — User Evidence Analysis in Memory

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 13  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Analyze a Windows memory image with Volatility 3 to identify artifacts associated with a user named Sarah.

The activity uses the memory image:

```text
memoria.img
```

The file is located in:

```text
/curso/aula13/memoria.img
```

The same memory image was used in previous practical exercises.

The investigation uses Volatility 3 plugins to identify operating system information, inspect environment variables, and search for file objects in memory.

The main objective is to identify user-related artifacts such as:

- User profile paths.
- Environment variables.
- File paths associated with the user.
- Temporary Internet Files.
- Process references associated with the user's profile.

The activity demonstrates how memory analysis can help identify user activity and correlate artifacts with a Windows account.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux forensic workstation |
| Memory Forensics Framework | Volatility 3 |
| Volatility Version | 2.7.0 |
| Memory Image | `memoria.img` |
| Image Source | `/curso/aula13/memoria.img` |
| Working Directory | `/home/aluno/coleta` |
| Operating System in Image | Windows XP |
| Windows Version | 5.1 |
| Build | 2600 |
| Service Pack | SP2 |
| Architecture | 32-bit |
| User of Interest | `Sarah` |
| Main Plugins | `windows.info`, `windows.envars`, `windows.filescan` |
| Filtering Utility | `grep` |

## 3. Memory Forensics and User Artifacts

### Memory-Based User Evidence

A memory image can preserve information associated with user activity.

Examples include:

- Environment variables.
- Process command lines.
- Open file objects.
- File paths.
- User-related application data.
- Browser and temporary file references.
- Credential-related artifacts.

These records can provide information that is not immediately apparent from an examination of the filesystem alone.

### Volatility 3

Volatility 3 is an open-source framework for memory forensic analysis.

It processes an acquired memory image and applies plugins to extract information about the operating system and its artifacts.

The general command structure used in the laboratory is:

```bash
volatility -f memoria.img plugin_name
```

The `-f` option identifies the input memory image.

The plugin name selects the type of analysis.

The activity uses the following Windows plugins:

| Plugin | Purpose |
|---|---|
| `windows.info` | Identifies Windows kernel and operating system information |
| `windows.pslist` | Lists processes present in memory |
| `windows.envars` | Examines process environment variables |
| `windows.filescan` | Scans for file objects present in memory |

### Environment Variables

Environment variables provide contextual information about a process.

A Windows process can inherit environment variables associated with the user session.

Examples include:

| Variable | Information |
|---|---|
| `HOMEPATH` | User profile path relative to the drive |
| `USERPROFILE` | Full user profile path |
| `USERNAME` | Account name |
| `TEMP` | Temporary directory |
| `PATH` | Executable search path |

The activity uses `HOMEPATH` to identify processes associated with Sarah's user profile.

### FileScan

The `windows.filescan` plugin searches a memory image for file objects.

It can identify references to files and paths that were present in memory.

The output may include file names, paths, and memory offsets.

Filtering the result for a specific username can help identify files associated with a particular profile.

## 4. Procedure

### Step 1 — Identify the Windows System in the Memory Image

The activity first establishes the operating system version represented in the memory image.

A root shell was opened:

```bash
sudo su
```

The working directory was accessed:

```bash
cd /home/aluno/coleta
```

The `windows.info` plugin was executed:

```bash
volatility -f memoria.img windows.info > windows_info.txt
```

The command components are:

| Component | Function |
|---|---|
| `volatility` | Starts the Volatility 3 command-line interface |
| `-f memoria.img` | Specifies the memory image |
| `windows.info` | Examines Windows kernel and system information |
| `>` | Redirects standard output to a file |
| `windows_info.txt` | Destination file for the plugin output |

The output was then displayed:

```bash
cat windows_info.txt
```

The supplied course output is:

```text
Volatility 3 Framework 2.7.0

Progress: 100.00 PDB scanning finished

Variable                     Value

Kernel Base                  0x804d7000
DTB                          0x39000
Symbols                      file:///opt/volatility3/volatility3/symbols/windows/ntoskrnl.pdb/32962337F0F646388B39535CD8DD70E8-2.json.xz
Is64Bit                      False
IsPAE                        False
layer_name                   0 WindowsIntel
memory_layer                 1 FileLayer
KdDebuggerDataBlock          0x8054c060
NTBuildLab                   2600.xpsp_sp2_gdr.050301-1519
CSDVersion                   2
KdVersionBlock               0x8054c038
Major/Minor                  15.2600
MachineType                  332
KeNumberProcessors           1
SystemTime                   2005-06-25 16:58:47
NtSystemRoot                 C:\WINDOWS
NtProductType                NtProductWinNt
NtMajorVersion               5
NtMinorVersion               1
PE MajorOperatingSystemVersion 5
PE MinorOperatingSystemVersion 1
PE Machine                   332
PE TimeDateStamp             Wed Mar 2 00:59:37 2005
```

The output identifies the image as a 32-bit Windows XP system.

Relevant fields include:

| Field | Value |
|---|---|
| Is64Bit | `False` |
| NTBuildLab | `2600.xpsp_sp2_gdr.050301-1519` |
| CSDVersion | `2` |
| NtMajorVersion | `5` |
| NtMinorVersion | `1` |
| NtSystemRoot | `C:\WINDOWS` |
| KeNumberProcessors | `1` |
| SystemTime | `2005-06-25 16:58:47` |

The system time is the time represented in the memory image, not the current workstation clock.

### Step 2 — Examine Plugin Help

Volatility provides a help option for individual plugins.

The activity used the following command:

```bash
volatility -f memoria.img windows.pslist -h
```

The supplied output is:

```text
Volatility 3 Framework 2.7.0

usage: volatility windows.pslist.PsList [-h] [--physical] [--pid [PID ...]] [--dump]

options:
  -h, --help            show this help message and exit
  --physical            Display physical offsets instead of virtual
  --pid [PID ...]       Process ID to include (all other processes are excluded)
  --dump                Extract listed processes
```

The help output identifies the options accepted by `windows.pslist`.

| Option | Function |
|---|---|
| `-h`, `--help` | Displays the plugin help |
| `--physical` | Displays physical offsets instead of virtual offsets |
| `--pid` | Includes only the specified process IDs |
| `--dump` | Extracts the listed processes |

This step demonstrates how plugin documentation can be accessed directly from the command line.

### Step 3 — Examine User Environment Variables

The next step examines environment variables associated with processes in the memory image.

The `windows.envars` plugin was executed:

```bash
volatility -f memoria.img windows.envars > envars.txt
```

The command saves the complete output to:

```text
envars.txt
```

To focus on the home path of the user, the following filter was applied:

```bash
cat envars.txt | grep HOMEPATH
```

The command pipeline works as follows:

| Component | Function |
|---|---|
| `cat envars.txt` | Displays the saved environment variable output |
| `|` | Sends the command output to the next command |
| `grep HOMEPATH` | Retains lines containing the text `HOMEPATH` |

The supplied output is:

```text
Volatility 3 Framework 2.7.0

1812 explorer.exe       0x00010000 HOMEPATH \Documents and Settings\Sarah
1936 Directcd.exe       0x00010000 HOMEPATH \Documents and Settings\Sarah
1952 TaskSwitch.exe     0x00010000 HOMEPATH \Documents and Settings\Sarah
1960 Fast.exe           0x00010000 HOMEPATH \Documents and Settings\Sarah
1980 VPTray.exe         0x00010000 HOMEPATH \Documents and Settings\Sarah
2040 atiptaxx.exe       0x00010000 HOMEPATH \Documents and Settings\Sarah
188  jusched.exe        0x00010000 HOMEPATH \Documents and Settings\Sarah
224  EM_EXEC.EXE        0x00010000 HOMEPATH \Documents and Settings\Sarah
2424 wuauclt.exe        0x00010000 HOMEPATH \Documents and Settings\Sarah
944  PluckSvr.exe       0x00010000 HOMEPATH \Documents and Settings\Sarah
2392 iexplore.exe       0x00010000 HOMEPATH \Documents and Settings\Sarah
2624 cmd.exe            0x00010000 HOMEPATH \Documents and Settings\Sarah
4012 dd.exe             0x00010000 HOMEPATH \Documents and Settings\Sarah
```

The result shows multiple processes with an environment variable referencing:

```text
\Documents and Settings\Sarah
```

The process names and IDs provide points for additional investigation.

### Step 4 — Search for File Objects Associated with Sarah

The activity then examines file objects found in the memory image.

The `windows.filescan` plugin was executed:

```bash
volatility -f memoria.img windows.filescan > filescan.txt
```

The output was redirected to:

```text
filescan.txt
```

The file scan results were filtered for references to Sarah:

```bash
cat filescan.txt | grep Sarah
```

The visible course extraction includes the following result:

```text
0x1340100 \Documents and Settings\Sarah\Local Settings\Temporary Internet Files\Content.IE5\D33YZADF\B1631076.5;abr=!ie;sz=300x250;ord=2005.06.25.16.50[1].38 112
```

The supplied text extraction ends with another memory offset:

```text
0x135f028
```

The remainder of that record and subsequent matching results are not present in the supplied text.

The original filescan output may contain additional records. They should be transcribed from the original terminal capture or PDF rather than reconstructed from partial text.

The visible record references the following path:

```text
\Documents and Settings\Sarah\Local Settings\Temporary Internet Files\Content.IE5\
```

This is a user-specific Internet Explorer temporary file directory.

The result demonstrates that file-system-related objects and paths can be identified through memory scanning.

## 5. Expected Results

The activity demonstrates the identification of user-related artifacts from the Windows memory image.

The important results are:

| Analysis | Result |
|---|---|
| `windows.info` | Identifies Windows XP SP2, 32-bit |
| `windows.pslist -h` | Displays process-list plugin options |
| `windows.envars` | Extracts process environment variables |
| `grep HOMEPATH` | Identifies multiple process references to Sarah's profile |
| `windows.filescan` | Searches memory for file objects |
| `grep Sarah` | Filters file paths containing Sarah |

The environment variable results identify multiple processes associated with:

```text
\Documents and Settings\Sarah
```

The filescan result includes a path under the user's Internet Explorer Temporary Internet Files directory.

## 6. Technical Analysis

### Operating System Identification

The initial `windows.info` analysis identifies the memory image as Windows XP SP2.

The important values are:

```text
Is64Bit       False
NTBuildLab    2600.xpsp_sp2_gdr.050301-1519
CSDVersion    2
NtMajorVersion 5
NtMinorVersion 1
```

This information is critical because Volatility plugins depend on operating system structures and supported memory layouts.

The image is not a modern Windows 10 or Windows 11 memory image. It represents a 32-bit Windows XP environment.

### Environment Variables as User Evidence

The `windows.envars` plugin identifies process environment variables.

The filter:

```bash
grep HOMEPATH
```

reduces the result to entries containing the specified profile path variable.

The output shows multiple processes using:

```text
\Documents and Settings\Sarah
```

The processes include:

```text
explorer.exe
Directcd.exe
TaskSwitch.exe
Fast.exe
VPTray.exe
atiptaxx.exe
jusched.exe
EM_EXEC.EXE
wuauclt.exe
PluckSvr.exe
iexplore.exe
cmd.exe
dd.exe
```

The result associates these process environment records with the Sarah profile path.

This does not by itself prove that Sarah personally initiated every process. It establishes that the memory image contains process environment information referencing that profile.

### FileScan Analysis

The `windows.filescan` plugin scans memory for file objects.

The resulting paths can provide evidence of files that were referenced or present in the memory structures at the time represented by the image.

Filtering for:

```text
Sarah
```

helps isolate results associated with the investigated user profile.

The visible record references Internet Explorer Temporary Internet Files.

This may support further examination of browser-related activity, but the file path alone does not establish the full contents or exact user action.

### Combining Envars and FileScan Results

The two analyses provide complementary information:

| Plugin | Evidence |
|---|---|
| `windows.envars` | Process environment variables referencing Sarah's profile |
| `windows.filescan` | File-object paths referencing Sarah's profile |

The correlation between process environment information and file paths provides a stronger investigative lead than examining either source independently.

### Plugin Help and Reproducibility

The command:

```bash
volatility -f memoria.img windows.pslist -h
```

demonstrates how the installed framework can expose plugin parameters.

This is useful because options and behavior can change between versions.

The plugin help should be checked when reproducing a procedure with a different Volatility release.

## 7. Results and Interpretation

The activity demonstrates how Volatility 3 can identify user-related artifacts in a Windows memory image.

The `windows.info` plugin identified the system as Windows XP SP2, 32-bit.

The environment variable scan returned multiple processes with:

```text
HOMEPATH \Documents and Settings\Sarah
```

The filescan filtering operation also identified a path under:

```text
\Documents and Settings\Sarah\Local Settings\Temporary Internet Files
```

These artifacts provide information about the user profile and files referenced in memory.

The results can be correlated with browser history and other recovered data during a broader investigation.

## 8. Concepts Practiced

- Memory forensics
- Volatility 3
- Windows memory images
- Windows XP SP2
- 32-bit memory analysis
- `windows.info`
- Plugin help
- `windows.pslist`
- `windows.envars`
- `windows.filescan`
- Environment variables
- `HOMEPATH`
- User profile identification
- File object scanning
- Temporary Internet Files
- `grep`
- Command output redirection
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 3 — PDF page 3 — Step 4.**

The screenshot should show:

```bash
cat filescan.txt | grep Sarah
```

The output should display file paths associated with the user profile.

The screenshot must show the personalized terminal prompt and the relevant memory scan results.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 13.3 is on page 3 of the consolidated PDF.

## References

- [Volatility 3 — Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 — Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
- [Volatility 3 — Windows Info](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.info.html)
- [Volatility 3 — Windows Environment Variables](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.envars.html)
- [Volatility 3 — Windows FileScan](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.filescan.html)
- [Volatility 3 — Windows PsList](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.pslist.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 13.4](../atividade-13.4-analise-processos-ativos/README.md)
