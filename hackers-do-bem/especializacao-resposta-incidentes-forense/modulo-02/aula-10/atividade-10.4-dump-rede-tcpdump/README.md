# Activity 10.4 - Network Dump with tcpdump

## Overview

This activity captures network traffic from the internal laboratory network using tcpdump.

The capture is restricted to traffic involving the `forenseLinux` host and is saved to a PCAP file for subsequent examination.

## Objectives

- Identify active network interfaces and assigned IP addresses.
- Capture network packets using tcpdump.
- Restrict the capture to a specific host.
- Limit the number of captured packets.
- Generate MD5 and SHA-256 hashes for the capture.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Capture Tool | tcpdump |
| Network Interface | `ens5` |
| Host Filter | `192.168.98.10` |
| Capture File | `captura.pcap` |

## Procedure

### 1. Inspect Network Interfaces

Run:

```bash
ip a
```

The course example identifies:

| Interface | Description | Address |
|---|---|---|
| `lo` | Loopback | `127.0.0.1` |
| `ens5` | Internal virtual network interface | `192.168.98.10/24` |

Actual interface names and addresses depend on the virtual machine configuration.

### 2. Capture Network Traffic

Open a root shell:

```bash
su root
```

Start the packet capture:

```bash
tcpdump -n -v host 192.168.98.10 -i ens5 -c 100 -w captura.pcap
```

The command parameters are:

| Option | Purpose |
|---|---|
| `-n` | Avoid resolving addresses and ports into names |
| `-v` | Enable verbose output |
| `host 192.168.98.10` | Capture packets matching the host filter |
| `-i ens5` | Select the network interface |
| `-c 100` | Stop after 100 matching packets |
| `-w captura.pcap` | Write captured packets to a PCAP file |

### 3. Verify the Capture

List the generated file:

```bash
ls -la
```

### 4. Generate Integrity Hashes

Calculate MD5:

```bash
md5sum captura.pcap > captura.pcap.md5
```

Calculate SHA-256:

```bash
sha256sum captura.pcap > captura.pcap.sha256
```

List the capture and hash files:

```bash
ls -la
```

## Expected Result

tcpdump captures up to 100 matching packets from the selected interface and writes them to `captura.pcap`.

MD5 and SHA-256 files are generated for integrity verification.

## Evidence

**Required screenshot: Step 2 - Print 3, PDF page 3.**

The required capture is the `ip a` output showing the active network interfaces, including `lo` and `ens5`, and their assigned IP addresses.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- `ip a` displays network interfaces and addresses.
- tcpdump supports packet capture filters and output to PCAP files.
- The `-c` option stops capture after the specified number of matching packets.
- The course example captures traffic involving the laboratory host.
- Only capture traffic in environments for which you have explicit authorization.
- Hashes should be retained with the PCAP file as part of the evidence record.

## References

- [tcpdump - Official Manual](https://www.tcpdump.org/manpages/tcpdump.1.html)
- [Linux - ip manual](https://man7.org/linux/man-pages/man8/ip.8.html)

## Navigation

- [Class 10](../README.md)
- [Previous Activity - 10.3](../atividade-10.3-evidencias-logicas-memoria/README.md)
- [Next Activity - 10.5](../atividade-10.5-evidencias-logicas-rede-wireshark/README.md)
