# Activity 13.5 — Network Artifacts in Memory

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 13  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Examine network-related artifacts preserved in a Windows memory image using Volatility.

Memory analysis can reveal network structures associated with TCP and UDP communications, including local and remote addresses, ports, protocol information, and connection state.

The activity focuses on identifying network activity represented in the acquired memory image.

The evidence description specifies a Volatility network plugin output showing established connections, open ports, and active IP addresses.

The objective is to understand how network artifacts recovered from memory can help reconstruct communications that existed at the time represented by the image.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux forensic workstation |
| Forensic Framework | Volatility 3 |
| Framework Version Identified | 2.7.0 |
| Memory Image | `memoria.img` |
| Working Directory | `/home/aluno/coleta` |
| Target Operating System | Windows XP SP2 |
| Target Architecture | 32-bit |
| Network Analysis | Volatility Windows network plugins |
| Relevant Plugin Family | `windows.netscan` / `windows.netstat` |

The target operating system was identified in Activity 13.3 using the `windows.info` plugin.

The corresponding output identifies Windows XP SP2, 32-bit.

## 3. Network Forensics Concepts

### Network Artifacts in Memory

A running Windows system maintains information about network activity in memory.

Depending on the operating system and the data structures preserved, these artifacts can include:

- Local IP addresses.
- Remote IP addresses.
- Local ports.
- Remote ports.
- TCP and UDP protocol information.
- Connection state.
- Process identifiers associated with connections.
- Timestamps or other object metadata.

These structures can help an investigator identify communication relationships that existed at the time represented by the memory image.

### Volatility Network Plugins

Volatility includes plugins designed to examine Windows network structures.

The relevant plugin names in current Volatility 3 include:

| Plugin | General Function |
|---|---|
| `windows.netscan` | Scans memory for network objects |
| `windows.netstat` | Traverses network tracking structures |

The exact plugin available and its compatibility depend on the Volatility version and target Windows build.

### Network Connection Fields

A network scan can return information such as:

| Field | Description |
|---|---|
| Offset | Memory address or object offset |
| Proto | Network protocol |
| LocalAddr | Local IP address |
| LocalPort | Local port |
| ForeignAddr | Remote IP address |
| ForeignPort | Remote port |
| State | Connection state |
| PID | Process identifier |
| Owner | Process or application name |
| Created | Timestamp associated with the network object, when available |

These fields help associate network activity with a process and identify the endpoints involved.

### TCP Connection States

TCP connections can be represented using states such as:

| State | Meaning |
|---|---|
| LISTENING | Application is waiting for incoming connections |
| ESTABLISHED | Connection has been established |
| TIME_WAIT | Connection is waiting before the local endpoint is reused |
| CLOSE_WAIT | Remote endpoint closed the connection and the local application has not fully closed it |
| CLOSED | Connection is no longer active |

The exact state values reported depend on the network objects recovered and the target operating system.

## 4. Procedure

### Step 1 — Access the Memory Analysis Working Directory

The Linux forensic workstation was used to examine the memory image.

The working directory is:

```bash
cd /home/aluno/coleta
```

The memory image used in the previous activities is:

```text
memoria.img
```

The operating system information previously obtained with:

```bash
volatility -f memoria.img windows.info
```

identifies the target as:

```text
Windows XP SP2
32-bit
```

This information is important when selecting a network analysis plugin.

### Step 2 — Identify the Available Network Plugin

Volatility provides plugin-specific help.

The available plugin list can be inspected with:

```bash
volatility --help
```

The plugin help can also be queried directly.

For the modern network scan plugin:

```bash
volatility -f memoria.img windows.netscan -h
```

For the network tracking plugin:

```bash
volatility -f memoria.img windows.netstat -h
```

These commands request plugin information rather than performing the complete network analysis.

The exact command used in the course evidence must be taken from the original terminal screenshot because the activity summary does not preserve the plugin command or its complete output.

### Step 3 — Examine Network Objects

The common Volatility 3 command for scanning supported Windows memory images is:

```bash
volatility -f memoria.img windows.netscan
```

The command components are:

| Component | Function |
|---|---|
| `volatility` | Starts Volatility 3 |
| `-f memoria.img` | Specifies the memory image |
| `windows.netscan` | Scans for Windows network objects |

When supported by the target Windows build, the plugin can report local and remote endpoints, protocol information, state, process identifiers, and other network metadata.

The activity's evidence description indicates that network output was examined for established connections, open ports, and IP addresses.

The actual IP addresses, port numbers, process identifiers, protocol values, and connection states are not included in the supplied activity text. They must be transcribed from the original PDF screenshot.

### Step 4 — Interpret the Network Results

The network output should be examined to identify:

- Local and remote IP addresses.
- Local and remote ports.
- TCP or UDP protocol information.
- Connection state.
- Process identifiers.
- Process names associated with the network structures.

The information can then be correlated with the process list from Activity 13.4.

For example, a PID identified in a network record can be compared with the process information obtained using:

```bash
volatility -f memoria.img windows.pslist
```

This correlation can help identify which process was associated with a network endpoint.

## 5. Expected Results

A successful network artifact analysis should provide information about network objects preserved in the memory image.

The relevant fields include:

| Information | Investigative Purpose |
|---|---|
| Local IP | Identifies the local endpoint |
| Local Port | Identifies the local service or endpoint port |
| Remote IP | Identifies the external endpoint |
| Remote Port | Identifies the destination service port |
| Protocol | Identifies TCP or UDP communication |
| State | Indicates the observed connection state |
| PID | Links the network object to a process |
| Owner | Provides process context, when available |

The results can be correlated with the process information from Activity 13.4.

## 6. Technical Analysis

### Network Analysis Depends on the Target Windows Version

The `windows.info` results from Activity 13.3 identify the memory image as:

```text
Windows XP SP2
Is64Bit: False
NTBuildLab: 2600.xpsp_sp2_gdr.050301-1519
NtMajorVersion: 5
NtMinorVersion: 1
```

This compatibility detail matters.

Current Volatility 3 `windows.netscan` support does not include Windows XP SP2.

The Volatility Foundation has explicitly confirmed that the modern `windows.netscan` plugin does not support Windows XP SP2.

The current `windows.netstat` implementation also depends on network scanning structures and should not be assumed to work with this XP image.

Therefore, a modern `windows.netscan` command cannot be presented as a confirmed successful operation against this specific memory image without checking the original laboratory evidence and framework version.

### Volatility 3 Versus Older Volatility Plugins

Older versions of Volatility provide different Windows network plugins.

The Volatility 2 framework includes plugins such as:

| Plugin | General Purpose |
|---|---|
| `connections` | Lists network connection objects |
| `connscan` | Scans memory for connection objects |
| `sockets` | Lists socket structures |
| `sockscan` | Scans memory for socket structures |

These plugins belong to the older Volatility framework and are not interchangeable with Volatility 3 plugin names.

The appropriate tool must be selected according to the target operating system and the framework version.

### Interpreting Connection State

A network artifact may represent a connection that was active, listening, or recently closed.

The state should be interpreted together with the capture time and other memory information.

A connection object remaining in memory does not automatically prove that the communication was active at the exact moment of acquisition.

### Correlating Network Objects with Processes

A PID in a network record can be compared with the process listing from Activity 13.4.

This correlation can help connect an endpoint to a process.

The resulting investigation can combine:

- User environment variables from Activity 13.3.
- File paths from Activity 13.3.
- Process identifiers from Activity 13.4.
- Network endpoints from this activity.

This creates a more complete view of the system's execution and communication context.

### Evidence and Compatibility Validation

The supplied activity summary identifies a network plugin output but does not include the exact plugin name, command, or returned rows.

Because the identified operating system is Windows XP SP2, the original screenshot should be checked before identifying the successful plugin as `windows.netscan` or `windows.netstat`.

The plugin name and output should be transcribed exactly as shown in the original evidence.

No IP addresses, ports, connection states, or process IDs are fabricated in this documentation.

## 7. Results and Interpretation

The activity focuses on identifying network artifacts preserved in a Windows memory image.

The evidence description specifies output related to established connections, open ports, and IP addresses.

These artifacts are useful because they can help reconstruct communications associated with the system and correlate network endpoints with processes.

The operating system identified in Activity 13.3 is Windows XP SP2, 32-bit. Current Volatility 3 network scanning plugins do not support this target version, so the exact plugin and successful output must be confirmed against the original activity screenshot.

## 8. Concepts Practiced

- Network forensics
- Memory-based network artifacts
- Volatility 3
- Windows network structures
- TCP
- UDP
- Local IP addresses
- Remote IP addresses
- Local and remote ports
- Connection states
- `windows.netscan`
- `windows.netstat`
- Process identifiers
- Network-to-process correlation
- Operating system compatibility
- Evidence interpretation

## 9. Evidence

**Required screenshot: Print 5 — PDF page 5 — Step 4.**

The screenshot should show the network artifact analysis output from the course activity.

The evidence description requires information about:

- Established connections.
- Open ports.
- IP addresses.
- Network-related memory artifacts.

The actual plugin name and output values should be read from the original screenshot.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 13.5 is on page 5 of the consolidated PDF.

## References

- [Volatility 3 — Official Documentation](https://volatility3.readthedocs.io/en/latest/)
- [Volatility 3 — Windows Tutorial](https://volatility3.readthedocs.io/en/latest/getting-started-windows-tutorial.html)
- [Volatility 3 — Windows NetScan](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.netscan.html)
- [Volatility 3 — Windows NetStat](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.windows.netstat.html)
- [Volatility Foundation — Windows XP NetScan Compatibility Discussion](https://github.com/volatilityfoundation/volatility3/issues/1847)
- [Volatility 2 — Official Project](https://github.com/volatilityfoundation/volatility)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
