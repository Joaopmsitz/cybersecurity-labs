# Activity 2.05 — Observing Microsoft Defender SmartScreen Protection Against a Keylogger Sample

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 05–06  
> **Environment:** Windows Server 2022 virtual lab  
> **Status:** Completed

## Objective

Explore how Windows security protections respond to a file associated with a **keylogger** in a controlled laboratory environment.

The activity used **Microsoft Defender SmartScreen** to observe the browser's response to an attempted download of a file containing a keylogger example.

The main objective was to understand how endpoint protection mechanisms can warn users about potentially unsafe downloads before the downloaded content is executed.

> **Safety notice:** This activity was performed exclusively for educational purposes in a laboratory environment. The file was not executed, and the keylogger was not installed or run.

## Environment

- **Operating system:** Windows Server 2022
- **Browser:** Microsoft Edge
- **Security feature:** Microsoft Defender SmartScreen
- **File manager:** Windows File Explorer
- **Execution environment:** Virtual machine
- **Source repository:** GitHub project containing the keylogger example used in the activity

## Procedure

### 1. Access the Windows Environment

The Windows Server 2022 virtual machine was started, and the desktop was accessed.

During the initial use of the system, a network discovery prompt appeared:

```text
Do you want to allow your PC to be discoverable by Other PCs and devices on this network?
```

The laboratory environment was configured according to the exercise instructions.

### 2. Access the Keylogger Repository

Microsoft Edge was opened, and the following GitHub repository was accessed:

```text
https://github.com/MinhasKamal/StupidKeylogger
```

The repository contains a project named **StupidKeylogger**, used in the activity to demonstrate a program designed to record keyboard input.

The repository was inspected to understand the purpose of the project before attempting to obtain the archive.

### 3. Open the Download URL

A new Microsoft Edge tab was opened to access the archive associated with the project:

```text
https://github.com/MinhasKamal/StupidKeylogger/archive/application.zip
```

The purpose of this step was to observe how the Windows security mechanisms would respond to an attempt to download the file.

### 4. Observe the Microsoft Defender SmartScreen Warning

During the download attempt, Microsoft Edge displayed the following warning:

```text
StupidKeylogger-application.zip was blocked as unsafe by Microsoft Defender SmartScreen.
```

This was the main result observed during the activity.

Microsoft Edge initially blocked the download and displayed a security warning. This demonstrated the operation of a browser-integrated protection mechanism designed to help users avoid potentially unsafe downloads.

**Technical note:** SmartScreen evaluates reputation and other risk signals associated with websites and downloaded files. A warning can indicate known malicious content or an unknown or insufficiently trusted download reputation. The warning alone does not establish that Microsoft Defender Antivirus specifically identified the file as a keylogger.

### 5. Inspect the Available Security Options

The browser's download warning provided additional options related to the file.

The additional options were accessed through the menu represented by three dots (`...`).

This step demonstrated how Microsoft Edge presents security information and additional controls when a download is classified as unsafe.

The activity focused on observing the protection interface. The file was not executed.

### 6. Observe the Additional Protection Message

After the interaction described during the exercise, Microsoft Edge displayed a second security message:

```text
This app is unsafe
```

This message provided an additional warning concerning the file.

The observed behavior demonstrated that security warnings can appear at different stages of the download and file-access process.

The warning should be interpreted as a security signal rather than independent proof of a specific malware classification.

### 7. Inspect the Downloads Folder

After the download-related steps in the exercise, Windows File Explorer was opened and the `Downloads` folder was inspected.

The following file was located:

```text
StupidKeylogger-application.zip
```

Its presence in the file system allowed the activity's result to be visually inspected.

This was the screenshot requested by the exercise.

The archive remained an object of analysis only. The keylogger was not installed or executed.

## Commands and Actions Used

Unlike the previous Kali Linux activities, this exercise was performed primarily through the Windows graphical interface.

The observed workflow was:

```text
Microsoft Edge
    |
    v
StupidKeylogger GitHub Repository
    |
    v
application.zip Download URL
    |
    v
Microsoft Defender SmartScreen
    |
    v
Security Warning
    |
    v
Additional Security Options
    |
    v
Downloads Folder
    |
    v
File Inspection
```

No terminal or PowerShell commands were required.

## Interpreting the Results

The activity demonstrated how Microsoft Defender SmartScreen can respond to a download associated with a keylogger sample.

The first warning displayed was:

```text
StupidKeylogger-application.zip was blocked as unsafe by Microsoft Defender SmartScreen.
```

A subsequent message displayed:

```text
This app is unsafe
```

These messages showed that the browser presented security warnings and applied a protective barrier during the download and file-access process.

Microsoft Defender SmartScreen uses reputation-based checks and other signals to assess potentially unsafe websites and downloaded applications. Its warnings can help users recognize risky downloads before running them.

However, it is important to distinguish among different security outcomes:

- **SmartScreen warning:** Indicates that a download or application presents a security concern based on reputation and other available signals.
- **Antivirus detection:** Indicates that an antivirus engine has identified a file as malicious or potentially unwanted according to its detection criteria.
- **Execution prevention:** Prevents or interrupts a file's execution, which is a separate outcome from a download warning.

The observed warning does not, by itself, prove that the file was scanned and specifically detected as a keylogger by Microsoft Defender Antivirus.

The experiment also reinforced the importance of user awareness. Users should treat unexpected security warnings seriously and avoid proceeding with files they cannot verify.

## Result

The activity demonstrated how to:

- Access the GitHub project used as the keylogger example.
- Identify the ZIP archive provided by the project.
- Attempt to download the archive through Microsoft Edge.
- Observe the Microsoft Defender SmartScreen warning.
- Inspect the additional security options in the browser.
- Observe the subsequent `This app is unsafe` message.
- Inspect the Windows `Downloads` folder.
- Locate the archive associated with the demonstration.
- Observe a preventive security mechanism without executing the keylogger.

The file was not executed during the activity.

## Concepts Practiced

- Microsoft Defender SmartScreen
- Endpoint security
- Keyloggers and malware risks
- Download reputation and security warnings
- Browser security
- Preventive protection
- Security alert interpretation
- File inspection
- Threat prevention
- User security awareness
- Safe handling of potentially malicious artifacts

## Evidence

The activity evidence is included in the PDF for Classes 05–06.

The relevant screenshots document the download attempt, the SmartScreen warning, the additional security message, and the file observed in the Downloads folder.

[View Evidence — Classes 05–06](../evidencias.pdf)

---

[Back to Classes 05–06](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
