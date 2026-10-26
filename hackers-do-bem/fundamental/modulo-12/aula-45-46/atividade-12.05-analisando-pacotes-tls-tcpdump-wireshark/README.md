# Activity 12.05 — Analyzing TLS Packets with tcpdump and Wireshark

## Objective

Capture and analyze HTTPS traffic using `tcpdump` and Wireshark, identify a TLS connection, and verify the protocol version used in the communication.

The activity uses the IPv4 address obtained through a DNS query for the `gov.br` domain to restrict the capture to HTTPS traffic destined for that address.

## Environment

- **Operating system:** Kali Linux
- **Tools:** `nslookup`, `tcpdump`, and Wireshark
- **Network interface:** `eth0`
- **Domain analyzed:** `gov.br`
- **Port:** `443`
- **Protocol:** TLS

## 1. Accessing Kali Linux

Kali Linux was started and accessed via RDP.

After logging in, a terminal was opened, and administrative privileges were obtained using:

```bash
sudo -i
```

## 2. Looking Up the IP Address of gov.br

Before starting the capture, a DNS query was performed to identify the IP address associated with the domain:

```bash
nslookup gov.br
```

Output:

```text
Server:         192.168.98.2
Address:        192.168.98.2#53

Non-authoritative answer:
Name:   gov.br
Address: 161.148.164.31
Name:   gov.br
Address: 2804:151:3:2:161:148:164:31
```

The query returned:

```text
IPv4: 161.148.164.31
IPv6: 2804:151:3:2:161:148:164:31
```

For the capture performed in this activity, the following IPv4 address was used:

```text
161.148.164.31
```

## 3. Preparing tcpdump

The command used to capture traffic was:

```bash
tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
```

The command was prepared in the terminal, but execution was postponed until the appropriate moment in the activity.

### Parameters Used

- **`tcpdump`:** A tool for capturing and analyzing packets.
- **`-i eth0`:** Captures traffic on the `eth0` interface.
- **`-s 0`:** Uses the maximum packet snapshot length, avoiding truncation of captured packet data by the snap length setting.
- **`host 161.148.164.31`:** Restricts the capture to the IPv4 address identified for `gov.br`.
- **`and port 443`:** Limits the capture to traffic associated with port `443`.
- **`-w capture.pcap`:** Saves the captured packets to the `capture.pcap` file.

This configuration focuses the capture on HTTPS traffic destined for the IPv4 address identified during the DNS query.

## 4. Preparing to Access the Website

With the `tcpdump` command prepared in the terminal, Firefox was opened.

The following address was entered in the browser:

```text
gov.br
```

The address was entered, but access was not initiated immediately.

## 5. Starting the Capture

Focus was returned to the terminal where the `tcpdump` command had been prepared.

The command was executed:

```bash
tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
```

`tcpdump` started capturing packets and displayed:

```text
┌──(root㉿kali)-[~]
└─# tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
```

At this point, `tcpdump` remained running, waiting for packets matching the configured filter.

## 6. Generating HTTPS Traffic

After starting the capture, focus was returned to Firefox.

Enter was pressed to access the domain:

```text
gov.br
```

The website loaded while `tcpdump` recorded packets associated with the HTTPS communication.

After the page finished loading, the browser was closed.

## 7. Stopping the Capture

Focus was returned to the terminal, and the capture was interrupted using:

```text
Ctrl+C
```

The displayed result was:

```text
^C3935 packets captured
3935 packets received by filter
0 packets dropped by kernel
```

The capture recorded:

- 3935 packets captured.
- 3935 packets received by the filter.
- 0 packets dropped by the kernel.

The capture file was saved as:

```text
capture.pcap
```

## 8. Verifying the Capture File

To verify that the file had been created, the following command was executed:

```bash
ls
```

Output:

```text
┌──(root㉿kali)-[~]
└─# ls
capture.pcap  Desktop    Downloads          Music     Public     Templates          Videos
curso        Documents   inicializacao.log  Pictures  Ransomware thinclient_drives
```

The presence of:

```text
capture.pcap
```

confirms that the capture was stored in the current directory.

## 9. Opening the Capture in Wireshark

The Wireshark application was opened.

From the top menu, the following option was selected:

```text
File → Open
```

The following file was then located and opened:

```text
capture.pcap
```

Wireshark loaded the packets recorded by `tcpdump`.

## 10. Filtering TLS Packets

The following filter was entered in the Wireshark filter bar:

```text
tls
```

The filter restricts the display to packets that Wireshark identifies as belonging to the TLS protocol.

## 11. Analyzing TLS Connections

After applying the filter, TLS connections present in the capture were examined.

For the packets analyzed, Wireshark may identify information related to TLS negotiation, including versions such as:

```text
TLS 1.2
TLS 1.3
```

Identifying the protocol version makes it possible to determine which TLS version is present in the captured packets.

In addition to the protocol version, Wireshark may display other session information, such as IP addresses, ports, handshake messages, and parameters related to cryptographic negotiation.

The capture was performed specifically for the IPv4 address `161.148.164.31` on port `443`, according to the filter used in `tcpdump`.

## 12. Evidence

The required screenshot corresponds to Step 12, showing the `capture.pcap` file open in Wireshark with the following filter:

```text
tls
```

The screen should display the TLS packets identified in the capture and their available information, including the protocol version when displayed by Wireshark.

**Caption to include before the screenshot:**

> Screenshot of Activity 12.05: the `capture.pcap` file open in Wireshark with the `tls` filter applied, displaying TLS connections and their versions, such as TLS 1.2 and/or TLS 1.3.

[**View Evidence — Module 12 / Classes 45–46**](../evidencias.pdf)

## 13. Removing the Capture File

After completing the analysis, Wireshark was closed.

The temporary capture file was removed using:

```bash
rm capture.pcap
```

Removing the file prevents the capture from being unnecessarily retained in the lab environment.

## Key Concepts

- **`tcpdump`:** A tool for capturing packets on network interfaces.
- **PCAP:** A file format used to store network traffic captures.
- **TLS:** A cryptographic protocol used to protect communications such as HTTPS.
- **Port 443:** The port commonly used for HTTPS.
- **Wireshark:** A graphical tool for detailed packet analysis.
- **`tls` filter:** A display filter used to focus on packets identified as TLS.

## Activity Workflow

```text
nslookup gov.br
        ↓
161.148.164.31
        ↓
tcpdump on eth0
        ↓
host 161.148.164.31 + port 443
        ↓
Access gov.br
        ↓
capture.pcap
        ↓
Wireshark
        ↓
Filter: tls
        ↓
Analyze TLS connections
```

## Result

HTTPS traffic destined for the IPv4 address `161.148.164.31`, obtained through `nslookup gov.br`, was captured.

`tcpdump` recorded 3935 packets, with no packet drops reported by the kernel, and stored the data in `capture.pcap`. The file was subsequently opened in Wireshark and analyzed using the `tls` filter, allowing the TLS connections present in the capture and their identified protocol versions to be examined.

---

[Back to Classes 45–46](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
