# Activity 8.5 - Ransomware Memory Analysis with Volatility 3

## Overview

This activity introduces memory forensics using Volatility 3. The practical exercise inspects a memory dump named `wcry.raw`, associated with a WannaCry ransomware incident, and identifies operating system information.

## Objectives

- Locate the provided memory image.
- Verify the presence of `wcry.raw`.
- Run the Volatility 3 `windows.info` plugin.
- Identify the operating system information contained in the memory image.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Forensic Framework | Volatility 3 |
| Working Directory | `/opt/volatility3` |
| Memory Image | `wcry.raw` |
| Plugin | `windows.info` |

## Procedure

### 1. Locate the Memory Image

Move to the Volatility 3 directory:

```bash
cd /opt/volatility3
```

List the directory contents:

```bash
ls
```

Confirm that `wcry.raw` is present.

### 2. Inspect the Memory Image

Run the `windows.info` plugin:

```bash
sudo python3 /opt/volatility3/vol.py -f /opt/volatility3/wcry.raw windows.info
```

Review the output for operating system and memory image information.

The course example identifies a Windows XP Service Pack 3 system.

## Expected Result

Volatility 3 processes the memory image and displays operating system information through the `windows.info` plugin.

## Evidence

**Required screenshot: Step 2 - Print 5, PDF page 5.**

The detailed screenshot specification for this class requests the Volatility 3 `windows.info` command and its output, showing the Windows XP SP3 identification.

Note: the course text also identifies the initial directory listing of `wcry.raw` as Step 2. The screenshot description supplied for this documentation specifies the `windows.info` result; follow the exact capture instruction provided by the course when assembling the final PDF.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Volatility 3 analyzes memory images using dedicated plugins.
- The `-f` option identifies the memory image to analyze.
- `windows.info` extracts operating system and kernel information.
- Additional plugins such as `windows.pslist`, `windows.pstree`, and `windows.psscan` can be used for further process investigation.
- Memory analysis results depend on image integrity, supported operating system structures, and symbol availability.

## References

- [Volatility 3 - Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 - Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
- [Volatility 3 - GitHub Repository](https://github.com/volatilityfoundation/volatility3)

## Navigation

- [Class 08](../README.md)
- [Previous Activity - 8.4](../atividade-8.4-hybrid-analysis/README.md)
- [Module 02](../../README.md)
