# Activity 2.03 — Exploring Ransomware Artifacts on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 05–06  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Explore a ransomware artifact-generation tool in a controlled laboratory environment, observe the available ransomware family labels, and inspect the resulting file in the Linux filesystem.

The activity focused on understanding how a tool can produce a potentially malicious artifact and how the generated file can be inspected without executing it.

> **Safety notice:** Ransomware can cause data loss, system disruption, and service unavailability. The artifact produced during this exercise was not executed. All observations were performed in a virtualized laboratory environment for educational purposes.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** Ransomware Creator
- **Runtime:** Python 3
- **File manager:** Thunar
- **Execution environment:** Virtualized laboratory

## Procedure

### 1. Open an Administrative Shell

The terminal was opened and an administrative shell was started:

```bash
sudo -i
```

### 2. Access the Tool Directory

The directory containing the laboratory tool was accessed:

```bash
cd /curso/Ransomware
```

The directory contents were inspected using:

```bash
ls
```

The Ransomware Creator was then opened in the laboratory environment. Its startup screen identified the tool as:

```text
RANSOMWARE CREATOR BY ERR0R

Ransomware Virus Creator Tools Version 1.0
DON'T Try to Use it on Your Computer!
```

### 3. Inspect the Available Commands

The tool's help interface was consulted to understand the available menu options.

The displayed commands included:

| Command | Purpose |
|---|---|
| `help` | Display usage information |
| `show` | List the ransomware labels available in the tool |
| `clear` | Clear the terminal interface |
| `menu` | Return to the main menu |
| `EXIT` | Close the program |

This step provided an overview of the tool's interface and functionality.

### 4. Review the Available Ransomware Labels

The listing function displayed references to multiple ransomware families, including:

- Cerber
- CryptoWall
- Jigsaw
- Locky
- Mamba
- Petya
- TeslaCrypt
- WannaCry
- Other entries provided by the tool

These names represent labels presented by the laboratory application. Their presence in the menu does not independently establish that the tool generates authentic samples of each named family.

### 5. Observe the Generated Artifact

During the laboratory exercise, the tool reported that it had completed artifact generation. Its output included the following information:

```text
Creating Ransomware
File name: Ransomware.WannaCry.zip
File type: .zip

[+] Loading... 100 % [success]

Completed
File saved as /sdcard
```

The output indicated that the operation had completed and reported `/sdcard` as the destination.

The tool labeled the generated artifact `Ransomware.WannaCry.zip`. This label was recorded as part of the laboratory output rather than treated as independent confirmation of the artifact's malware family.

### 6. Inspect the Filesystem

A second terminal was used to inspect the root directory:

```bash
cd /
ls
```

The listing included an entry named:

```text
sdcard
```

This entry was subsequently located using the Thunar file manager.

The artifact was inspected visually to verify the result of the preceding operation.

### 7. Identify the Executable

During the inspection, a file with the `.exe` extension and an approximate size of 3.5 MB was observed at the reported output location.

The executable was identified as part of the artifact produced during the exercise.

**Important:** The file was inspected but never opened or executed. No attempt was made to encrypt files, modify a target system, or test ransomware behavior.

### 8. Handle the Artifact Safely

After the inspection, the laboratory activity was concluded without executing the artifact.

Potentially malicious files should remain isolated from production systems and personal data. Any further analysis should take place in an appropriately isolated environment using established malware-analysis procedures.

## Commands Used

The documented filesystem inspection commands were:

```bash
sudo -i
cd /curso/Ransomware
ls

cd /
ls
```

The tool interface was used to review the available functionality and observe the artifact-generation result. The generated file was not executed.

## Interpreting the Results

The exercise demonstrated a basic stage in the handling of potentially malicious software: the creation and subsequent inspection of a file that may require security analysis.

The observed workflow was:

```text
Ransomware Creator
        |
        v
Artifact Generation Report
        |
        v
Filesystem Inspection
        |
        v
Executable Identified
        |
        v
No Execution Performed
```

The artifact's name and file extension were not sufficient to establish its true behavior or family attribution. Reliable identification would require additional evidence, such as cryptographic hashes, static analysis, and results from reputable malware-analysis services.

The main distinction demonstrated by this activity was the difference between identifying a potentially malicious artifact and executing it. The laboratory stopped at the inspection stage, avoiding the operational risks associated with running ransomware.

## Result

The activity provided experience in:

- Exploring the interface of a ransomware artifact-generation tool
- Reviewing the labels presented for different ransomware families
- Observing the tool's reported generation result
- Inspecting the Linux filesystem for the resulting artifact
- Identifying a Windows executable during the inspection
- Distinguishing an artifact label from verified malware attribution
- Completing the exercise without executing the file

The activity reinforced the importance of treating suspicious executable files as potentially dangerous and examining them only under appropriate safety controls.

## Concepts Practiced

- Ransomware and malware artifacts
- WannaCry as a ransomware-family reference
- Suspicious executable identification
- Linux filesystem navigation
- Thunar file inspection
- Malware-analysis fundamentals
- Safe handling of potentially malicious files
- Virtualized laboratory environments
- Endpoint security
- Threat identification and evidence documentation

## Evidence

The activity evidence is included in the PDF for Classes 05–06.

The relevant screenshots document the tool interface, its reported output, and the subsequent filesystem inspection.

[View Evidence — Classes 05–06](../evidencias.pdf)

---

[Back to Classes 05–06](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
