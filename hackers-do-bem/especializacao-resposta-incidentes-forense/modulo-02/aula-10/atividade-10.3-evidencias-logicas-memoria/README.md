# Activity 10.3 — Windows Memory Analysis with Volatility 3

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 02  
> **Class:** 10  
> **Environment:** Linux forensic analysis workstation  
> **Status:** Completed

## 1. Objective

Analyze the Windows memory image acquired in Activity 10.2 using Volatility 3.

The activity introduces memory analysis through Volatility plugins that examine Windows kernel information and extract account-related password hash material from a memory image.

The investigation begins by identifying operating system information from the memory image using the `windows.info` plugin.

The exercise also demonstrates the use of the Hashdump plugin to examine credential-related artifacts stored in a Windows memory image.

## 2. Environment

| Item | Details |
|---|---|
| Forensic Framework | Volatility 3 |
| Analysis Environment | Linux forensic workstation |
| Source Artifact | Windows memory image acquired in Activity 10.2 |
| Operating System Under Examination | Windows |
| Analysis Type | Memory forensics |
| Information Plugin | `windows.info` |
| Legacy Hashdump Plugin | `windows.hashdump` |
| Current Hashdump Plugin | `windows.registry.hashdump` |

The exact filename and filesystem path of the Windows memory image are not preserved in the activity notes supplied for this documentation. The commands therefore use a clearly marked image-path placeholder.

## 3. Memory Analysis Concepts

### Memory Image Analysis

A memory image is a snapshot of the contents of RAM captured from a running or recently active system.

Memory analysis can provide information about the operating system, processes, loaded modules, network activity, and other artifacts.

The image acquired in Activity 10.2 is used as the input source for this activity.

### Volatility 3

Volatility 3 is an open-source memory forensics framework.

It provides plugins that interpret operating system structures and extract artifacts from memory images.

Unlike FTK Imager, Volatility is not the acquisition tool used in this class. It receives an existing memory image and performs analysis against it.

The general command structure is:

```bash
python3 vol.py -f <memory_image> plugin_name
```

The `-f` option identifies the memory image to be examined, and `plugin_name` specifies the analysis plugin.

### Windows Information Plugin

The `windows.info` plugin examines Windows kernel information and reports details about the operating system structures identified in the memory image.

The output can include information useful for identifying the Windows version, architecture, kernel, and symbol requirements.

### Hashdump Plugin

The Hashdump plugin extracts local account password hashes from Windows memory artifacts.

The resulting values are sensitive authentication material. They should be treated as forensic evidence and protected accordingly.

The course exercise uses the legacy Windows Hashdump implementation. Current Volatility 3 documentation identifies `windows.registry.hashdump` as the replacement for the deprecated implementation.

## 4. Procedure

### Step 1 — Identify the Windows Memory Image

The Windows memory image acquired in Activity 10.2 was selected as the input for analysis.

The file must be accessible from the environment in which Volatility 3 is executed.

The exact image filename and location are not reproduced because they were not included in the activity details available for this README.

### Step 2 — Run the Windows Information Plugin

The operating system information was examined with:

```bash
python3 vol.py -f <memory_image> windows.info
```

Replace `<memory_image>` with the actual path to the image acquired in Activity 10.2.

The command components are:

| Component | Function |
|---|---|
| `python3` | Starts the Python 3 interpreter |
| `vol.py` | Volatility 3 command-line interface |
| `-f` | Specifies the input memory image |
| `<memory_image>` | Path to the Windows memory image |
| `windows.info` | Analyzes Windows kernel and operating system information |

The plugin processes the memory image and reports the Windows information that can be identified.

The values returned depend on the memory image and the symbols successfully resolved by Volatility.

### Step 3 — Examine the Windows Information Output

The `windows.info` output is used to identify the operating system context represented by the memory image.

Relevant fields can include:

| Field | Forensic Purpose |
|---|---|
| Kernel Base | Identifies the kernel's base address in memory |
| Directory Table Base | Provides information about the kernel address translation context |
| Is64Bit | Indicates whether the analyzed operating system is 64-bit |
| NT Build Lab | Provides build information |
| CSD Version | Provides service pack information when available |
| System Time | Indicates the system time represented in the memory image |
| PE Information | Provides details associated with the Windows kernel image |

These fields help establish the environment represented by the memory image and provide context for subsequent plugin execution.

The supplied activity summary does not preserve the literal output values, so no kernel addresses, build numbers, or timestamps are invented in this documentation.

### Step 4 — Execute the Hashdump Analysis

The activity also uses the Windows Hashdump plugin to examine local account hash material.

The legacy plugin is invoked in the course procedure using:

```bash
python3 vol.py -f <memory_image> windows.hashdump
```

The memory image supplied with `-f` must be the same Windows image used in the previous step.

The plugin examines the available Windows memory and registry-related structures to identify local account hash information.

### Step 5 — Interpret the Hashdump Results

The Hashdump output can contain account-related fields such as:

- Username.
- User identifier (RID).
- LM hash, when available.
- NT hash.

These values are dependent on the Windows image being analyzed.

The actual usernames and hash values were not included in the activity notes available for this documentation. They should be transcribed from the original terminal output or evidence capture rather than replaced with sample credentials.

## 5. Expected Results

The activity demonstrates two different types of memory analysis:

| Plugin | Expected Result |
|---|---|
| `windows.info` | Windows kernel and operating system information |
| `windows.hashdump` | Local account hash material available in the memory image |

The first plugin establishes the system context.

The second plugin demonstrates how credential-related artifacts can be extracted from a Windows memory image.

## 6. Technical Analysis

### Why the Memory Image Is Required

Volatility 3 works against an acquired memory image.

The memory acquisition itself was performed in Activity 10.2 with FTK Imager.

The two activities represent separate stages of the forensic workflow:

```text
Live Windows System
        |
        v
   FTK Imager
        |
        v
Windows Memory Image
        |
        v
   Volatility 3
        |
        +----------------------+
        |                      |
        v                      v
  windows.info           windows.hashdump
        |                      |
        v                      v
 System Context       Account Hash Material
```

This separation is important because acquiring evidence and interpreting evidence are different forensic operations.

### Windows.info

The `windows.info` plugin provides context about the Windows image.

This is useful when identifying the operating system structures that Volatility has successfully recognized.

The information can also help troubleshoot symbol resolution or compatibility problems when analyzing different Windows builds.

### Hashdump and Current Plugin Naming

The course exercise uses the legacy Hashdump implementation.

The older plugin implementation is documented under:

```text
volatility3.plugins.windows.hashdump.Hashdump
```

The Volatility 3 documentation marks this implementation as deprecated and identifies the registry-based implementation as its replacement.

The replacement plugin name is:

```text
windows.registry.hashdump
```

A current equivalent command is:

```bash
python3 vol.py -f <memory_image> windows.registry.hashdump
```

The legacy command is preserved in this report as part of the historical laboratory procedure. The replacement command is documented separately to prevent confusion when using newer Volatility 3 versions.

### Handling Credential Material

Password hashes extracted from memory are sensitive artifacts.

They should not be published in public documentation unless their disclosure is explicitly justified and authorized.

For this portfolio, the purpose of the exercise is to document the use of the plugin and its forensic role, not to expose authentication material from the laboratory image.

## 7. Results and Interpretation

The activity demonstrates the use of Volatility 3 to examine a Windows memory image acquired with FTK Imager.

The `windows.info` plugin provides operating system and kernel context, while the Hashdump plugin demonstrates the extraction of local account hash material.

Together, these operations show how memory images can be used to obtain information that supports incident investigation and forensic reconstruction.

The activity also exposes an important versioning consideration: the legacy Hashdump implementation has been deprecated in current Volatility 3 documentation, and the registry-based plugin should be used for new workflows.

## 8. Concepts Practiced

- Windows memory forensics
- Volatility 3
- Memory image analysis
- Windows kernel information
- Operating system identification
- Symbol resolution
- `windows.info`
- Password hash extraction
- Hashdump plugin
- Plugin deprecation and replacement
- Handling sensitive forensic artifacts
- Memory acquisition and analysis workflow

## 9. Evidence

The class evidence PDF consolidates the screenshots required by the practical activities.

[View Universal Class Evidence PDF](../evidences.pdf)

The exact page number for this activity is not specified in the activity notes available for this documentation.

## References

- [Volatility 3 — Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 — Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
- [Volatility 3 — Deprecated Windows Hashdump Implementation](https://volatility3.readthedocs.io/en/stable/_modules/volatility3/plugins/windows/hashdump.html)
- [Volatility 3 — Registry Hashdump Plugin](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.registry.hashdump.html)

---

[Back to Class 10](../README.md) · [Back to Module 02](../../README.md) · [Back to Specialization](../../../README.md)
