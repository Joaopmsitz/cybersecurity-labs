# Intro to Network Traffic Analysis

> HTB Academy — Basic Toolset

## Overview

Network traffic analysis examines packet captures to understand communication patterns, protocols, connection behavior, and possible security events.

## Useful Wireshark Display Filters

| Purpose | Filter |
|---|---|
| Find traffic involving an IP | `ip.addr == <ip-address>` |
| DNS traffic | `dns` |
| HTTP traffic | `http` |
| TCP connection initiation | `tcp.flags.syn == 1 && tcp.flags.ack == 0` |
| Traffic for a specific port | `tcp.port == <port>` |

## Tcpdump Reference

| Objective | Example |
|---|---|
| Read a capture file | `tcpdump -nn -r capture.pcap` |
| Read a capture and filter by host | `tcpdump -nn -r capture.pcap host <ip-address>` |
| Read a capture and filter by port | `tcpdump -nn -r capture.pcap port <port>` |

## Key Concepts

- Packet headers and protocol fields
- Ethernet, IP, TCP, UDP, DNS, and HTTP
- Source and destination addresses
- TCP handshakes and connection resets
- Filters versus capture filters
- Identifying unusual communication patterns

## Practical Workflow

1. Preserve the original capture.
2. Identify the relevant hosts and time range.
3. Filter traffic by protocol, IP, or port.
4. Follow relevant conversations and inspect packet details.
5. Build a timeline and record evidence with timestamps.

## Lab Notes

Document the capture examined, filters used, notable packets, and conclusions supported by the evidence.

## References

- [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
- [Tcpdump manual](https://www.tcpdump.org/manpages/tcpdump.1.html)
