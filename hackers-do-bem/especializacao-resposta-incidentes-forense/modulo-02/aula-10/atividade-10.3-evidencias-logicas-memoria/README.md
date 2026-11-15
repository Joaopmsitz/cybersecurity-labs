# Activity 10.3 - Logical Memory Evidence Collection

## Overview

This activity uses Volatility 3 to extract forensic artifacts from a Windows memory image.

The practical exercise examines the supplied `memoria.img` file and runs plugins to identify system information, processes, registry hives, command-line activity, and file artifacts.

## Objectives

- Prepare a working directory for memory analysis.
- Copy the supplied memory image.
- Identify the operating system using `windows.info`.
- Extract selected forensic artifacts using Volatility 3 plugins.
- Preserve results in separate output files.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Forensic Framework | Volatility 3 |
| Source Image | `/curso/aula10/memoria.img` |
| Working Directory | `/home/aluno/coleta` |
| Main Plugin | `windows.info` |

## Procedure

### 1. Prepare the Collection Directory

Open a root shell:

```bash
sudo su
```

Create the working directory:

```bash
mkdir /home/aluno/coleta
cd /home/aluno/coleta
```

Copy the supplied memory image:

```bash
cp /curso/aula10/memoria.img .
```

### 2. Identify the Operating System

Run the `windows.info` plugin and save the output:

```bash
volatility -f memoria.img windows.info > windows_info.txt
```

Display the results:

```bash
cat windows_info.txt
```

The course sample identifies a Windows XP system. The output includes kernel, architecture, memory layer, and operating system metadata.

### 3. Extract Additional Memory Artifacts

The course procedure includes the `windows.hashdump.Hashdump` plugin:

```bash
volatility -f memoria.img windows.hashdump.Hashdump > hashdump.txt
```

The generated file may contain password hashes. Treat it as sensitive forensic evidence and do not publish it in a public repository.

Other plugins in the practical exercise include:

Environment variables:

```bash
volatility -f memoria.img windows.envars.Envars > envars.txt
```

Process listing:

```bash
volatility -f memoria.img windows.pslist.PsList > pslist.txt
```

Registry hive listing:

```bash
volatility -f memoria.img windows.registry.hivelist.HiveList > hivelist.txt
```

Command-line information:

```bash
volatility -f memoria.img windows.cmdline.CmdLine > cmdline.txt
```

File scanning:

```bash
volatility -f memoria.img windows.filescan.FileScan > filescan.txt
```

### 4. Review the Generated Results

Inspect the output files relevant to the investigation:

```bash
ls -lh
```

Review the system metadata:

```bash
cat windows_info.txt
```

Additional analysis can be performed by selecting appropriate Volatility plugins according to the investigation requirements.

## Expected Result

Volatility 3 identifies the operating system information in the memory image and generates separate output files for the selected forensic artifacts.

The course example identifies Windows XP Service Pack 2 from the `windows.info` output.

## Evidence

**Required screenshot: Step 3 - Print 2, PDF page 2.**

The terminal screenshot must show:

- The personalized prompt.
- The execution of `volatility -f memoria.img windows.info`.
- The generated `windows_info.txt` output.
- The operating system and memory metadata returned by the plugin.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Volatility 3 uses symbol tables rather than the legacy profile mechanism used by Volatility 2.
- `windows.info` provides operating system and kernel information.
- `windows.pslist` enumerates process structures.
- `windows.cmdline` extracts process command-line information.
- `windows.filescan` scans memory for file objects.
- The course command uses the `volatility` executable supplied by the laboratory. Current upstream instructions also document the `vol` command and `python vol.py` invocation.
- The current Volatility 3 documentation marks `windows.hashdump.Hashdump` as deprecated.
- Memory images and extracted credential hashes must be handled as confidential evidence. Do not commit `memoria.img`, `hashdump.txt`, or other sensitive raw outputs.

## References

- [Volatility 3 - Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 - GitHub Repository](https://github.com/volatilityfoundation/volatility3)
- [Volatility 3 - Windows Hashdump Plugin](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.windows.hashdump.html)

## Navigation

- [Class 10](../README.md)
- [Previous Activity - 10.2](../atividade-10.2-dump-memoria-windows/README.md)
- [Next Activity - 10.4](../atividade-10.4-dump-rede-tcpdump/README.md)
