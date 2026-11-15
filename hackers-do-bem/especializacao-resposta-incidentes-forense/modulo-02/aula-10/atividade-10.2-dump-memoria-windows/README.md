# Activity 10.2 — Windows Memory Dump with FTK Imager

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 02  
> **Class:** 10  
> **Environment:** Windows forensic workstation  
> **Status:** Completed

## 1. Objective

Acquire volatile memory from a running Windows system using FTK Imager.

The activity demonstrates the acquisition of RAM from a live Windows workstation and the preparation of the resulting forensic image for later examination.

Unlike disk imaging, which collects data stored on persistent storage, memory acquisition captures information available while the operating system is running.

The resulting image can be examined with memory forensic tools such as Volatility 3, which is used in the subsequent activity.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | Windows forensic workstation |
| Operating System | Windows |
| Acquisition Tool | FTK Imager |
| Acquisition Type | Live memory acquisition |
| Evidence Type | Volatile memory |
| Application Menu | File → Capture Memory |
| Output | Windows memory image |
| Subsequent Analysis | Volatility 3 |

The exact destination path and output filename are not included in the activity notes available for this documentation. They should be read from the actual FTK Imager configuration or the acquired image.

## 3. Memory Acquisition Concepts

### Volatile Memory in Windows

Windows uses RAM to store data required by active processes and the operating system.

During an incident investigation, memory can contain relevant artifacts such as:

- Running process information.
- Loaded modules and drivers.
- Active network connections.
- Command execution artifacts.
- Data associated with user sessions.
- Information that may not be available in ordinary files on disk.

The contents of RAM are temporary. Shutting down or restarting a system can destroy information that might be relevant to an investigation.

### FTK Imager

FTK Imager is a forensic acquisition and examination utility.

The application provides a memory capture function that can acquire RAM from a live system.

The acquisition procedure is accessed through:

```text
File → Capture Memory...
```

The Memory Capture dialog allows the examiner to configure the destination path and filename, along with optional collection settings.

### Memory Capture Configuration

The capture dialog can expose the following options:

| Option | Function |
|---|---|
| Destination path | Defines the directory used to save the acquired data |
| Destination filename | Defines the name of the memory image |
| Include pagefile | Includes the Windows pagefile in the collection |
| Create AD1 file | Creates an additional AD1 evidence container |

These options are separate from the RAM capture itself.

The activity notes available for this documentation do not preserve the exact checkbox state or destination filename used during the laboratory execution. Therefore, those settings are not presented as confirmed selections.

## 4. Procedure

### Step 1 — Access the Windows Forensic Workstation

The Windows forensic workstation was accessed to perform the live memory acquisition.

The FTK Imager application was used to capture memory from the running Windows system.

Memory acquisition requires elevated privileges because the application needs access to system memory.

The application should therefore be opened using the administrative context provided for the laboratory.

### Step 2 — Open FTK Imager

After accessing the workstation, FTK Imager was opened.

The application provides a graphical interface for forensic image acquisition and examination.

The memory capture functionality is available from the main menu.

### Step 3 — Open the Memory Capture Function

Within FTK Imager, the memory acquisition function is accessed through:

```text
File → Capture Memory...
```

Selecting this option opens the Memory Capture dialog.

The dialog is used to configure the output destination and acquisition settings before starting the capture.

### Step 4 — Configure the Destination

The Memory Capture dialog contains the following fields and options:

| Field | Description |
|---|---|
| Destination path | Directory where the acquired memory data will be stored |
| Destination filename | Name assigned to the memory image |
| Include pagefile | Optional collection of the Windows pagefile |
| Create AD1 file | Optional creation of an AD1 evidence container |

The destination path and filename must be selected before the acquisition begins.

For forensic work, an external or dedicated evidence destination is preferable to writing the acquired image to the same system volume being investigated. This reduces unnecessary writes to the source system and helps preserve evidence.

The exact path, filename, and option selections used in the laboratory should be taken from the actual capture configuration. They are not inferred in this documentation.

### Step 5 — Start the Memory Capture

After configuring the destination, the acquisition is initiated using the capture control in FTK Imager:

```text
Capture Memory
```

FTK Imager begins reading the live system memory and writing the result to the selected destination.

A progress indicator is presented while the acquisition is running.

The acquisition duration depends on the amount of memory and the system environment.

The activity notes do not contain a verbatim completion message or exact duration, so no specific progress output is reproduced here.

### Step 6 — Verify the Acquisition Result

After the capture process finishes, the destination directory should be inspected to confirm that the memory image was created.

The image is the primary artifact required for the next activity, where Volatility 3 is used to examine Windows memory structures.

The exact output filename and file size depend on the destination and the machine used in the laboratory.

## 5. Expected Results

The activity produces a Windows memory image at the destination selected in FTK Imager.

The expected result is:

| Artifact | Description |
|---|---|
| Memory image | Acquired snapshot of the live Windows system memory |
| Optional pagefile | Additional file collected when the pagefile option is selected |
| Optional AD1 container | Additional evidence container when that option is selected |

The memory image is subsequently used as input for the analysis performed in Activity 10.3.

## 6. Technical Analysis

### Live Acquisition

The acquisition is performed while Windows is running.

This is important because the contents of RAM are volatile and can disappear when the system is shut down.

The acquisition itself also interacts with the running system and may cause changes to its memory state. Forensic procedures should therefore document the time of acquisition and the tool configuration.

### RAM Image and Pagefile

RAM and the pagefile are related but distinct sources of information.

RAM is physical volatile memory. The pagefile is a disk-based Windows paging file used by the memory management system.

If the pagefile is included, the collection contains additional information from a persistent file. It should not be confused with the physical memory image itself.

### Why FTK Imager Is Used Before Volatility

FTK Imager performs acquisition.

Volatility 3 performs analysis of an acquired memory image.

The tools therefore have complementary roles:

| Tool | Role |
|---|---|
| FTK Imager | Acquires the Windows memory image |
| Volatility 3 | Examines operating system structures and memory artifacts |

Volatility does not replace the acquisition procedure performed by FTK Imager.

### Evidence Preservation

After acquisition, the memory image should be preserved and protected against accidental modification.

A forensic workflow should record the destination, filename, acquisition time, examiner, tool version, and integrity values when available.

The activity summary does not preserve the exact output filename, destination path, or hash values, so these values are not fabricated in this report.

## 7. Results and Interpretation

This activity demonstrates how FTK Imager can acquire volatile memory from an active Windows workstation.

The process begins with administrative access, followed by the use of the Capture Memory function and configuration of the output destination.

Once the acquisition completes, the resulting memory image becomes the input artifact for subsequent memory analysis.

The activity establishes the acquisition stage of the Windows memory forensics workflow. The next activity uses Volatility 3 to examine the collected image.

## 8. Concepts Practiced

- Windows memory acquisition
- Volatile memory
- Live forensic acquisition
- FTK Imager
- Administrative privileges
- Memory Capture dialog
- Pagefile collection
- AD1 evidence container
- Evidence destination management
- Forensic image preservation
- Memory acquisition and analysis workflow

## 9. Evidence

The activity information available for this class indicates that Activity 10.2 did not require a dedicated screenshot for the consolidated submission.

The consolidated class evidence remains available here:

[View Universal Class Evidence PDF](../evidences.pdf)

## References

- [Exterro — FTK Imager](https://www.exterro.com/digital-forensics-software/ftk-imager)
- [CISA — Memory Capture with FTK Imager](https://content.govdelivery.com/accounts/USDHSCISA/bulletins/2c5011c)
- [Volatility 3 — Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)

---

[Back to Class 10](../README.md) · [Back to Module 02](../../README.md) · [Back to Specialization](../../../README.md)
