# Activity 10.4 — Network Dump with tcpdump

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 02  
> **Class:** 10  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Identify the network interfaces available on the Linux forensic workstation and acquire network packets using tcpdump.

The activity introduces command-line packet capture and demonstrates how network traffic can be preserved in a PCAP file for subsequent examination.

The `ip a` command is used to inspect the available interfaces and their network configuration before selecting the capture interface.

The resulting packet capture can later be opened in Wireshark, which is used in Activity 10.5.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux |
| Interface Inspection | `ip a` |
| Packet Capture Tool | tcpdump |
| Capture Type | Network packet capture |
| Output Format | PCAP |
| Subsequent Analysis Tool | Wireshark |

The exact interface name and PCAP filename are not preserved in the activity summary available for this README. They should be taken from the original terminal execution rather than assumed.

## 3. Network Capture Concepts

### Network Interfaces

A network interface is the system component through which a machine sends and receives network traffic.

Linux can expose several interfaces, including:

- Loopback interfaces.
- Ethernet interfaces.
- Virtual machine network adapters.
- Wireless interfaces.
- Other virtual or tunnel interfaces.

Before capturing packets, the examiner must identify which interface is associated with the traffic being investigated.

### The `ip a` Command

The following command was used to inspect the available interfaces:

```bash
ip a
```

The command is a shorthand form of:

```bash
ip address show
```

It displays the interfaces and their assigned network addresses.

The output can include:

| Field | Meaning |
|---|---|
| Interface name | Name assigned to the network interface |
| Interface flags | Operational and configuration state |
| `link/ether` | Hardware or MAC address on Ethernet interfaces |
| `inet` | IPv4 address and prefix |
| `inet6` | IPv6 address and prefix |
| `mtu` | Maximum Transmission Unit |

The interface names and IP addresses depend on the virtual machine's network configuration.

### tcpdump

tcpdump is a command-line packet analyzer that captures and displays network traffic.

It can capture packets from a selected interface and save the raw packet data to a file.

The `-i` option specifies the network interface.

The `-w` option writes captured packet data to a file rather than displaying decoded packet details on the terminal.

This makes tcpdump useful for collecting traffic that will be examined later with Wireshark.

### PCAP Files

PCAP is a common format used to preserve packet capture data.

A PCAP file stores captured packet records and metadata required by packet analysis tools.

The file can be opened in Wireshark for protocol dissection, filtering, stream reconstruction, and object extraction.

## 4. Procedure

### Step 1 — Inspect the Network Interfaces

Before starting the capture, the available network interfaces were inspected:

```bash
ip a
```

This command displays the network interfaces configured on the Linux system.

The output should be examined to identify the interface associated with the traffic to be captured.

Typical information displayed includes:

- Interface identifier and name.
- Interface state.
- MAC address, when available.
- IPv4 address.
- IPv6 address.
- Network prefix.
- MTU.

The actual interface names, addresses, and flags are environment-specific. They should be transcribed from the original `ip a` screenshot rather than replaced with generic or invented values.

### Step 2 — Select the Capture Interface

After inspecting the output, the network interface used for packet capture was selected.

The interface name must match an interface shown by `ip a`.

The command structure for packet capture is:

```bash
sudo tcpdump -i <interface> -w <capture-file>.pcap
```

Replace:

- `<interface>` with the interface identified during the previous step.
- `<capture-file>.pcap` with the output filename used for the activity.

These placeholders are intentional because the activity notes supplied for this documentation do not preserve the exact interface name or filename.

### Step 3 — Start Packet Capture

tcpdump is executed with the selected interface and output file:

```bash
sudo tcpdump -i <interface> -w <capture-file>.pcap
```

The options used are:

| Option | Function |
|---|---|
| `sudo` | Executes tcpdump with elevated privileges |
| `tcpdump` | Starts the packet capture utility |
| `-i` | Selects the network interface |
| `<interface>` | Interface being monitored |
| `-w` | Writes packet data to a capture file |
| `<capture-file>.pcap` | Destination PCAP filename |

When writing to a file with `-w`, tcpdump stores packet data for later analysis rather than presenting the full decoded packet details on the terminal.

The capture remains active until it is stopped by the operator or reaches another configured stopping condition.

### Step 4 — Stop the Capture and Review the Summary

After the required traffic has been captured, the capture process is stopped from the terminal, normally by pressing:

```text
Ctrl+C
```

When tcpdump terminates, it reports capture statistics.

The summary can include lines with the following structure:

```text
<packet-count> packets captured
<packet-count> packets received by filter
<packet-count> packets dropped by kernel
```

These lines represent the structure of the statistics reported by tcpdump. The values depend on the actual capture and are not reproduced as literal results because they were not included in the supplied activity notes.

### Step 5 — Preserve the PCAP File

The resulting PCAP file is the artifact used in the subsequent Wireshark activity.

The file should be preserved without modification so that the packet capture can be analyzed separately.

The exact output filename and size must be taken from the laboratory's actual terminal or file listing.

## 5. Expected Results

The activity produces a PCAP file containing the network packets captured from the selected interface.

The expected workflow is:

```text
Linux Network Interfaces
        |
        v
      ip a
        |
        v
Select Capture Interface
        |
        v
     tcpdump
        |
        v
   PCAP File
        |
        v
   Wireshark
```

The capture file is used as the input artifact for Activity 10.5.

## 6. Technical Analysis

### Why Inspect the Interfaces Before Capturing?

A Linux system may have several network interfaces.

Capturing from the wrong interface can result in an empty or incomplete packet capture.

The `ip a` output provides the information needed to identify available interfaces and their assigned addresses.

The screenshot of this command is also useful as evidence of the network configuration of the laboratory machine at the time of the activity.

### tcpdump and the `-i` Option

The `-i` option selects the interface from which tcpdump reads packets.

The selected interface determines which traffic is visible to the capture process.

The interface name must therefore be taken from the actual output of `ip a`, not assumed from another virtual machine or host configuration.

### tcpdump and the `-w` Option

The `-w` option writes raw packet data to a file.

This differs from the default behavior, in which tcpdump prints a textual packet summary.

The saved capture can be opened by other packet analysis tools, including Wireshark.

The PCAP file preserves the captured traffic for later inspection without requiring the analyst to repeat the original capture.

### Capture Statistics

The statistics printed after stopping tcpdump provide a summary of the acquisition.

They can help an analyst understand how many packets were captured and whether the kernel reported dropped packets.

The statistics should be recorded with the evidence because packet loss can affect the completeness of a network investigation.

## 7. Results and Interpretation

The activity demonstrates the process of identifying Linux network interfaces and capturing network traffic with tcpdump.

The `ip a` command provides visibility into the network configuration of the forensic workstation.

After selecting the appropriate interface, tcpdump records network packets into a PCAP file.

The saved file provides the basis for the next activity, in which Wireshark is used to inspect traffic and export HTTP objects.

## 8. Concepts Practiced

- Linux network interfaces
- `ip a`
- IPv4 and IPv6 addressing
- MAC addresses
- Network interface state
- tcpdump
- Packet capture
- Interface selection
- PCAP format
- Packet capture statistics
- Network evidence preservation
- Network traffic analysis

## 9. Evidence

The activity requires a screenshot showing the network interface information obtained with:

```bash
ip a
```

The screenshot should preserve the output used to identify the available network interfaces.

The actual interface names, IP addresses, MAC addresses, and interface states should be read from the original evidence image.

[View Universal Class Evidence PDF](../evidences.pdf)

The PDF consolidates the screenshots submitted for the practical activities in Class 10.

## References

- [tcpdump — Linux Manual Page](https://www.man7.org/linux/man-pages/man1/tcpdump.1.html)
- [ip — Linux Manual Page](https://www.man7.org/linux/man-pages/man8/ip.8.html)
- [Wireshark — Official Documentation](https://www.wireshark.org/docs/)

---

[Back to Class 10](../README.md) · [Back to Module 02](../../README.md) · [Back to Specialization](../../../README.md)
