# Activity 2.03 — Exploring Ransomware Artifacts on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 05–06  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Explore a ransomware artifact-generation tool in a controlled laboratory environment, review the available ransomware family labels, generate an artifact, and inspect the resulting file in the Linux filesystem.

The activity focused on understanding the tool's interface, observing the generation process, and identifying the resulting artifact without executing it.

> **Safety notice:** Ransomware can cause data loss, system disruption, and service unavailability. The artifact generated during this exercise was not executed. All observations were performed in a virtualized laboratory environment for educational purposes.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** Ransomware Creator
- **Runtime:** Python 3
- **File manager:** Thunar
- **Execution environment:** Virtualized laboratory

## Procedure

### 1. Open an Administrative Shell

The terminal was opened, and an administrative shell was started:

```bash
sudo -i
```

### 2. Access the Tool Directory

The directory containing the ransomware creation tool was accessed:

```bash
cd /curso/Ransomware
```

The directory contents were checked with:

```bash
ls
```

The tool was launched using Python 3:

```bash
python3 Ransomware
```

After initialization, the application displayed the following banner and version information:

```text
██████╗  █████╗ ███╗   ██╗███████╗ ██████╗ ███╗   ███╗
██╔══██╗██╔══██╗████╗  ██║██╔════╝██╔══██╗████╗ ████║
██████╔╝███████║██╔██╗ ██║███████╗██║   ██║██╔████╔██║
██╔══██╗██╔══██║██║╚██╗██║╚════██║██║   ██║██║╚██╔╝██║
██║  ██║██║  ██║██║ ╚████║███████║╚██████╔╝██║ ╚═╝ ██║
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝╚══════╝ ╚═════╝ ╚═╝     ╚═╝

           RANSOMWARE CREATOR BY ERR0R

Ransomware Virus Creator Tools Version 1.0
DON'T Try to Use it on Your Computer!
```

### 3. Inspect the Available Commands

The tool's help interface was accessed using:

```text
Ransomware®Creator~> help
```

The application displayed the following menu:

```text
----------------------------------
| Commands            Description|
----------------------------------
| Help                How to Use |
| Show      Show List Ransomware |
| Clear             Clear window |
| Menu              Back to Menu |
| EXIT              Exit Program |
----------------------------------
```

This output identified the main commands available in the tool's interactive interface.

### 4. List the Available Ransomware Families

The `show` command was used to display the ransomware labels available in the application:

```text
Ransomware®Creator~> show
```

The following output was observed:

```text
This Files are Very Sensitive
Be Careful While You Using Them !

01. Ransomware.Cerber
02. Ransomware.Cryptowall
03. Ransomware.Jigsaw
04. Ransomware.Locky
05. Ransomware.Mamba
06. Ransomware.Matsnu
07. Ransomware.Petrwrap
08. Ransomware.Petya
09. Ransomware.Radamant
10. Ransomware.Rex
11. Ransomware.Satana
12. Ransomware.TeslaCrypt
13. Ransomware.Vipasana
14. Ransomware.WannaCry
15. Ransomware.WannaCry_Plus
```

The list demonstrated that the tool presented multiple ransomware family names as available options.

**Technical note:** These are the names displayed by the tool. Their presence in the menu does not independently establish that the generated artifacts are authentic samples of the corresponding malware families.

### 5. Inspect the Root Directory Before Generation

A second terminal was opened to observe the filesystem during the activity.

The root directory was accessed:

```bash
cd /
```

The following command was executed:

```bash
ls
```

Before artifact generation, the output showed the standard system directories:

```text
bin   curso  etc   lib   lost+found  mnt  proc  run   snap  sys  usr
boot  dev    home  lib64 media       opt  root  sbin  srv   tmp  var
```

This listing served as a reference for comparison with the filesystem after the generation process.

### 6. Observe the WannaCry-Labeled Artifact Generation

Back in the first terminal, option `14`, corresponding to the WannaCry-labeled entry, was selected in the tool's menu:

```text
Ransomware®Creator~> 14
```

The tool then displayed the following output:

```text
Creating Ransomware
File name: Ransomware.WannaCry.zip
File type: .zip

[+] Loading... 100 % [success]

Completed
File saved as /sdcard
For back to main menu, type: menu
```

The tool reported that the generation process had completed and identified `/sdcard` as the output location.

The reported filename was:

```text
Ransomware.WannaCry.zip
```

The artifact was treated only as an object for inspection. It was not executed.

### 7. Verify the Filesystem After Generation

In the second terminal, the root directory was listed again:

```bash
ls
```

The output now included the `sdcard` entry:

```text
bin   curso  etc   lib   lost+found  mnt  proc  run   sdcard  srv  tmp  var
boot  dev    home  lib64  media       opt  root  sbin  snap    sys  usr
```

The appearance of `sdcard` in this listing confirmed that the filesystem entry was present after the tool reported completing the generation process.

### 8. Inspect the Artifact with Thunar

The Thunar file manager was opened to visually inspect the filesystem.

The root path was accessed:

```text
/
```

The entry named `sdcard` was located and opened for inspection.

During this step, an executable file with the `.exe` extension and an approximate size of **3.5 MB** was observed.

The file was associated with the artifact-generation exercise.

> **Important:** The executable was only identified and inspected. It was not opened or executed, and no ransomware behavior was tested on a Windows system.

## Commands and Interactions Used

The terminal commands recorded during the activity were:

```bash
sudo -i
cd /curso/Ransomware
python3 Ransomware
```

To inspect the root directory before and after generation:

```bash
cd /
ls
```

The following inputs were entered into the tool's interactive interface:

```text
help
show
14
```

Here, `help`, `show`, and `14` were inputs to the running application, not shell commands.

The artifact was inspected visually using Thunar.

## Filesystem Structure Observed

The root directory initially displayed standard filesystem entries, including:

```text
bin
curso
etc
home
root
tmp
usr
```

After the tool reported completing generation, the listing also included:

```text
sdcard
```

The generated artifact was reported at:

```text
/sdcard
```

The tool's output identified the artifact as:

```text
Ransomware.WannaCry.zip
```

During the subsequent visual inspection, a `.exe` file of approximately 3.5 MB was identified.

The supplied laboratory record does not establish that the executable was an authentic WannaCry sample. Its name and reported size alone are insufficient to confirm its contents or behavior.

## Interpreting the Results

The laboratory demonstrated a basic stage in the handling of potentially malicious software: reviewing an artifact-generation tool, observing its output, and inspecting the resulting filesystem entry.

The observed workflow was:

```text
Ransomware Creator
        |
        v
Tool Banner and Main Interface
        |
        v
Review of Available Family Labels
        |
        v
Selection of the WannaCry-Labeled Option
        |
        v
Generation Report
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

The tool displayed a list of ransomware-related names and reported successful artifact generation after the WannaCry-labeled option was selected.

The subsequent `ls` output showed the `sdcard` entry in the root directory. Thunar was then used to inspect the reported location and identify an executable file.

The observations demonstrate the importance of distinguishing between:

- A tool's menu labels and verified malware identification
- A reported generation result and independently confirmed file contents
- Identifying a suspicious executable and executing it

A filename, extension, or approximate file size does not establish the exact functionality of an artifact. Reliable identification would require additional evidence, such as cryptographic hashes, static analysis, and results from reputable malware-analysis tools.

The laboratory stopped at the inspection stage, avoiding the operational risks associated with executing ransomware.

## Result

The activity provided experience in:

- Starting the Ransomware Creator application.
- Reviewing its banner and version information.
- Inspecting the available commands through `help`.
- Listing the ransomware family labels through `show`.
- Observing the tool's generation report for option `14`.
- Recording the reported filename and output location.
- Comparing the root directory listings before and after generation.
- Inspecting the resulting filesystem entry using Thunar.
- Identifying an `.exe` file of approximately 3.5 MB.
- Completing the inspection without executing the artifact.

The exercise demonstrated how a potentially malicious artifact can be generated and identified within a laboratory workflow, and why such files must be treated as unsafe until properly analyzed.

## Concepts Practiced

- Ransomware and malware artifacts
- Ransomware family names and attribution
- Ransomware Creator
- WannaCry as a family reference
- Suspicious executable identification
- Linux filesystem navigation
- Command output interpretation
- Thunar file inspection
- Malware-analysis fundamentals
- Safe handling of potentially malicious files
- Virtualized laboratory environments
- Endpoint security and threat identification

## Evidence

The activity evidence is included in the PDF for Classes 05–06.

The relevant screenshots document the tool's banner, help output, ransomware family listing, generation message, filesystem listing, and subsequent artifact inspection.

[View Evidence — Classes 05–06](../evidencias.pdf)

---

[Back to Classes 05–06](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
