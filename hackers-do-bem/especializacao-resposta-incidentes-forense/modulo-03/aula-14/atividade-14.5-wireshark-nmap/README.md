# Activity 14.5 — Network Attack Analysis with Wireshark

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 14  
> **Environment:** Wireshark workstation  
> **Status:** Completed

## 1. Objective

Analyze network traffic in Wireshark to identify indicators of a sequential Nmap port scan.

The activity uses a display filter based on the TCP window field:

```text
tcp.window_size_value == 1024
```

The filtered packets are then examined in the packet list, with the **Info** column sorted to make the observed scan sequence easier to inspect.

The course evidence identifies a scan involving 2,000 distinct ports.

The objective is to understand how a repeated packet pattern and sequential destination port activity can provide evidence of network reconnaissance.

## 2. Environment

| Item | Details |
|---|---|
| Analysis Tool | Wireshark |
| Protocol | TCP |
| Display Filter | `tcp.window_size_value == 1024` |
| Relevant TCP Field | Window |
| Packet List Column | Info |
| Observed Activity | Nmap port scan |
| Recorded Port Count | 2,000 distinct ports |
| Analysis Type | Offline network traffic inspection |

The exact packet capture filename, host addresses, destination port range, and individual packet numbers are not preserved in the supplied activity summary.

## 3. Technical Concepts

### Network Reconnaissance

Network reconnaissance is the process of collecting information about systems and services in a network.

Port scanning is a common reconnaissance technique used to determine which destination ports are open, closed, or filtered.

A scan may generate repeated connection attempts toward a target host.

### Nmap

Nmap is a network discovery and security auditing tool.

It supports several scanning methods, including:

- TCP SYN scan.
- TCP connect scan.
- UDP scan.
- Other specialized scan techniques.

The TCP SYN scan is commonly used to identify TCP port states without completing a full TCP connection in the usual manner.

### TCP Window Field

The TCP header contains a Window field.

This value advertises the amount of data the receiver is currently willing to accept.

Wireshark exposes the raw TCP header value as:

```text
tcp.window_size_value
```

Wireshark also exposes a calculated window size:

```text
tcp.window_size
```

These fields are not identical.

The `tcp.window_size_value` field represents the raw value carried in the TCP header.

### Wireshark Display Filters

A display filter limits the packets presented in the packet list.

The filter used in this activity is:

```text
tcp.window_size_value == 1024
```

It selects packets whose raw TCP window field equals 1024.

The filter does not independently prove that a packet belongs to an Nmap scan.

It is an indicator that must be correlated with other packet characteristics and the sequence of observed traffic.

### Packet List and Info Column

Wireshark's packet list presents information about captured frames.

The Info column displays a summary of the packet's protocol-specific details.

Sorting this column can help group similar packet descriptions and inspect repeated network behavior.

For a port scan, the analyst should also examine destination ports, TCP flags, source and destination addresses, and packet chronology.

## 4. Procedure

### Step 1 — Open the Network Capture

Wireshark was opened and the network capture supplied by the course was loaded.

The capture contains the traffic used to demonstrate network reconnaissance and scanning activity.

The exact capture filename and endpoint addresses are not included in the supplied activity summary.

### Step 2 — Apply the TCP Window Display Filter

The following display filter was entered in Wireshark:

```text
tcp.window_size_value == 1024
```

The filter selects packets where the raw TCP window value is exactly:

```text
1024
```

The field can be inspected in the TCP header within the Packet Details pane.

### Step 3 — Sort the Info Column

The packet list was organized by the **Info** column.

Sorting helps identify repeated packet descriptions and inspect the pattern of traffic associated with the scan.

The analysis should also consider the Destination Port field and the packet timestamps.

Sorting by Info is a presentation aid; it does not replace chronological analysis.

### Step 4 — Examine the Scan Pattern

The filtered packet list was examined for repeated TCP packets directed toward different destination ports.

The recorded evidence identifies a sequential and large-scale scan involving:

```text
2,000 distinct ports
```

The pattern is consistent with the Nmap reconnaissance activity described by the course.

The exact source IP, target IP, port sequence, packet numbers, and TCP flag values are not included in the supplied activity summary.

Those details should be transcribed from the original Wireshark evidence rather than invented.

## 5. Expected Results

The activity demonstrates the identification of repeated TCP traffic associated with a port scan.

| Item | Result |
|---|---|
| Tool | Wireshark |
| Display Filter | `tcp.window_size_value == 1024` |
| Raw TCP Window Value | 1024 |
| Relevant Column | Info |
| Observed Activity | Nmap port scan |
| Recorded Ports | 2,000 distinct ports |

The result provides an example of how network traffic patterns can reveal reconnaissance behavior.

## 6. Technical Analysis

### Interpretation of the TCP Window Value

The filter:

```text
tcp.window_size_value == 1024
```

selects packets with a raw TCP Window field equal to 1024.

A repeated value can be useful as a traffic characteristic when examining a known network scan pattern.

However, the value alone is not proof that Nmap generated the traffic.

Other applications or operating systems may also advertise the same TCP window value.

The field must be interpreted together with the packet sequence and other indicators.

### Nmap SYN Scan Behavior

Nmap supports TCP SYN scanning.

A SYN scan sends TCP SYN packets toward selected ports and interprets the responses to infer the state of each port.

Common response patterns include:

| Target Response | Typical Interpretation in a SYN Scan |
|---|---|
| SYN/ACK | Port is open |
| RST | Port is closed |
| No response or certain ICMP errors | Port may be filtered |

The exact interpretation depends on the response, filtering behavior, and scanning context.

### Why 1024 Can Be Relevant

The TCP window value may be used as one characteristic when analyzing a known Nmap scan pattern.

The filter in this activity selects packets with a value of 1024.

This is a useful starting point for narrowing the packet list, but it should not be used as a standalone signature for Nmap.

The investigator should corroborate the result with:

- Repeated SYN packets.
- A common source IP.
- A consistent target IP.
- Multiple distinct destination ports.
- Sequential port progression.
- Short intervals between attempts.
- Relevant TCP response patterns.

### Sequential Port Scanning

A scan of many distinct destination ports can indicate an attempt to discover available services on a target.

A sequence involving 2,000 distinct ports is consistent with automated reconnaissance rather than an isolated application connection.

The destination port sequence should be checked in the packet details and timestamps.

### Why the Info Column Helps

Sorting the Info column makes repeated packet descriptions easier to examine.

For a scan, however, the Info column may not display every detail needed to reconstruct the port sequence.

The analyst should also inspect the TCP and IP fields in the Packet Details pane and use sorting or additional display filters when necessary.

### Detection Limitations

A TCP window value of 1024 is not unique to Nmap.

A reliable identification of a scan should use multiple indicators and correlation.

The analysis should not classify every packet matching the filter as malicious.

The purpose of this activity is to identify the specific scan pattern in the supplied capture.

## 7. Results and Interpretation

The activity demonstrates how Wireshark can be used to identify network reconnaissance patterns.

The filter:

```text
tcp.window_size_value == 1024
```

reduces the packet list to frames containing the selected raw TCP window value.

The Info column is organized to make repeated packet descriptions easier to inspect.

The recorded evidence identifies a sequential Nmap scan involving 2,000 distinct ports.

The result demonstrates how traffic patterns, TCP fields, and destination port sequences can be used together to identify scanning behavior.

## 8. Concepts Practiced

- Network forensics
- Wireshark
- TCP analysis
- TCP header
- TCP window field
- `tcp.window_size_value`
- Display filters
- Packet list analysis
- Info column
- Network reconnaissance
- Port scanning
- Nmap
- TCP SYN scan
- Destination ports
- Sequential scanning
- Traffic pattern analysis
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 3 — PDF page 5.**

The screenshot should display Wireshark with the following display filter:

```text
tcp.window_size_value == 1024
```

The **Info** column should be sorted as described in the activity.

The packet list should show the sequential scan pattern and support the recorded finding of 2,000 distinct destination ports.

The exact IP addresses, destination port range, packet numbers, and TCP flag values should remain visible in the original evidence.

[View Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 14.5 is on page 5 of the consolidated PDF.

## References

- [Wireshark — TCP Display Filter Reference](https://www.wireshark.org/docs/dfref/t/tcp.html)
- [Wireshark — Display Filter Manual](https://www.wireshark.org/docs/man-pages/wireshark-filter.html)
- [Wireshark Wiki — Display Filters](https://wiki.wireshark.org/DisplayFilters/)
- [Nmap — Port Specification and Scan Order](https://nmap.org/book/man-port-specification.html)
- [Nmap — Port Scanning Techniques](https://nmap.org/book/man-port-scanning-techniques.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
