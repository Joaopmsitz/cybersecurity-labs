# Activity 2.02 — Exploring the XSPY Keylogger on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 05–06  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Explore the basic operation of the XSPY keylogger in a controlled laboratory environment.

The activity demonstrates how a keylogger can monitor keyboard events during execution and store captured output in a text file for subsequent analysis.

> **Safety notice:** This activity was performed exclusively for educational purposes in a controlled laboratory environment. The keylogger was used only to demonstrate its operation and was not used to capture information from third parties.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** XSPY
- **Text editor:** Kali Linux graphical text editor
- **Execution environment:** Virtualized laboratory

## Procedure

### 1. Navigate to the Working Directory

The terminal was opened, and the Documents directory was accessed:

```bash
cd /home/aluno/Documentos
```

The contents of the directory were checked using:

```bash
ls
```

At the beginning of the activity, the `teste.log` file did not exist in the directory.

### 2. Start XSPY

XSPY was started from the terminal, with its standard output redirected to `teste.log`:

```bash
xspy >> teste.log
```

The `>>` operator appends standard output to a file, creating the file if it does not already exist.

During the demonstration, XSPY began recording keyboard events within the laboratory environment.

### 3. Type Test Text

While XSPY was running, the Kali Linux text editor was opened.

The following phrase was typed manually:

```text
Hacker do bem!
```

The text was entered directly through the keyboard rather than being copied and pasted, allowing the experiment to observe the resulting keyboard events.

### 4. Stop XSPY

After the test text was entered, the terminal was accessed again and XSPY was stopped using:

```text
Ctrl + C
```

The terminal showed that the running process had been interrupted.

No additional keyboard monitoring was performed after the demonstration ended.

### 5. Verify the Captured Output File

The directory contents were checked again:

```bash
ls
```

The resulting listing included:

```text
teste.log
```

The file's presence confirmed that the output had been redirected to the Documents directory.

### 6. Review the Recorded Events

The file was opened in the terminal using:

```bash
cat teste.log
```

The observed output was similar to:

```text
opened :10.0 for snoopng

Shift_L hacker do bemShift_L 1Control_L c
```

The exact output depended on the laboratory environment and the keyboard events captured during execution.

The output did not necessarily reproduce the typed phrase exactly as it appeared in the text editor. Some events were represented by key names, including `Shift_L` and `Control_L`.

Despite these differences, the recorded output contained a recognizable sequence corresponding to the test phrase.

This demonstrated that the tool could record keyboard-related events and make the resulting output available for later review.

### 7. Remove the Test File

After reviewing the captured output, the test file was deleted:

```bash
rm teste.log
```

The directory was then checked again:

```bash
ls
```

The `teste.log` file was no longer present.

Removing the test file prevented the captured laboratory data from remaining unnecessarily in the working directory.

## Commands Used

The principal commands used during the activity were:

```bash
cd /home/aluno/Documentos
ls
xspy >> teste.log
```

The running process was stopped using `Ctrl + C`.

The output was then inspected and the test file removed:

```bash
ls
cat teste.log
rm teste.log
ls
```

## Interpreting the Results

The experiment demonstrated the basic operation of a keylogger, a tool capable of recording keyboard events.

The observed workflow was:

```text
Keyboard Events
       |
       v
      XSPY
       |
       v
   teste.log
       |
       v
  cat teste.log
       |
       v
Review of Recorded Events
```

The command:

```bash
xspy >> teste.log
```

redirected the program's standard output to a file, allowing the recorded output to be reviewed after execution had stopped.

The subsequent use of `cat` demonstrated that the redirected output remained available in the file after XSPY was terminated.

The laboratory also showed that recorded keyboard events may be represented differently from the original text, depending on the environment and the way the tool reports those events.

## Result

The activity demonstrated how to:

- Access the directory used to store the laboratory output.
- Start XSPY in the virtualized environment.
- Redirect the program's output to `teste.log`.
- Enter controlled test text through the keyboard.
- Stop the running process with `Ctrl + C`.
- Verify that the output file had been created.
- Review the recorded events using `cat`.
- Remove the test file after the experiment.

The exercise illustrated how keylogging tools can record keyboard-related activity and retain captured output for subsequent analysis.

## Concepts Practiced

- Keyloggers and keyboard event monitoring
- XSPY
- Keyboard input capture
- Output redirection with `>>`
- Log and text file handling
- Linux terminal operations
- Use of `ls`, `cat`, and `rm`
- Endpoint security
- Privacy and safe handling of captured data

## Evidence

The activity evidence is included in the PDF for Classes 05–06.

The relevant screenshot documents the XSPY test, the contents of `teste.log`, and the recorded keyboard events.

[View Evidence — Classes 05–06](../evidencias.pdf)

---

[Back to Classes 05–06](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
