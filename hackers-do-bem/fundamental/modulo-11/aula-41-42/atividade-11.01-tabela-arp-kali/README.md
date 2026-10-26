# Activity 11.01 — Exploring the ARP Table on Kali Linux

## Objective

Explore the ARP table on Kali Linux by examining the IP and MAC addresses associated with devices on the network, clearing existing entries, and verifying how new entries are learned again after network communication.

## Environment

- **Operating system:** Kali GNU/Linux
- **Access:** RDP
- **Network interface:** `eth0`
- **Tools:** Terminal, `arp`, and `ip`
- **Browser:** Mozilla Firefox

## 1. Accessing Kali Linux

The Kali Linux machine was started and accessed via RDP.

After connecting, a terminal was opened and administrative privileges were obtained with:

```bash
sudo -i
```

The system requested the user's password to elevate privileges:

```text
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:
```

## 2. Displaying the ARP Table

The following command was used to display the current ARP table entries:

```bash
arp -a
```

The output was:

```text
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-168-98-1.ec2.internal (192.168.98.1) em 12:82:f4:28:c9:8d [ether] em eth0
ip-192-168-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

The table shows the associations between IP addresses and MAC addresses known to the system.

### Observed Elements

- **`192.168.98.201`:** IP address associated with MAC address `12:5c:9d:d7:39:31`.
- **`192.168.98.1`:** IP address associated with MAC address `12:82:f4:28:c9:8d`.
- **`192.168.98.2`:** IP address associated with MAC address `12:82:f4:28:c9:8d`.
- **`[ether]`:** Indicates Ethernet as the link-layer technology.
- **`eth0`:** The network interface through which the association is known.

The ARP table allows the system to associate IPv4 addresses with their corresponding MAC addresses on the local network.

## 3. Clearing the ARP Table

The following command was executed to remove existing entries from the neighbor table:

```bash
ip -s -s neigh flush all
```

The output was:

```text
192.168.98.201 dev eth0 lladdr 12:5c:9d:d7:39:31  ref 1 used 66/0/66probes 1 REACHABLE
192.168.98.1 dev eth0 lladdr 12:82:f4:28:c9:8d  used 419/419/376probes 1 STALE
192.168.98.2 dev eth0 lladdr 12:82:f4:28:c9:8d  used 37/37/13probes 1 STALE

*** Round 1, deleting 3 entries ***
*** Flush is complete after 1 round ***
```

The command removed the learned entries from the neighbor table.

The states displayed before removal also provide information about the status of the associations, such as:

- **`REACHABLE`:** The neighbor is considered reachable.
- **`STALE`:** The entry exists but may need to be validated again when used.

## 4. Checking the ARP Table Again

After clearing the table, the command was executed again:

```bash
arp -a
```

The output was:

```text
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-168-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

The entry corresponding to `192.168.98.1` was no longer present at that moment.

The missing entry demonstrates the effect of clearing the table. Other entries may reappear when the system communicates with the corresponding destinations again.

## 5. Accessing Google

Mozilla Firefox was opened through the following menu:

```text
Applications → Web Browser
```

The following website was accessed:

https://www.google.com

This connection generates network traffic that may require the system to resolve link-layer information to reach the destination through the local network.

## 6. Checking the ARP Table Again

After accessing Google, the command was executed again:

```bash
arp -a
```

The output was:

```text
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-1.ec2.internal (192.168.98.1) em 12:82:f4:28:c9:8d [ether] em eth0
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

The entry corresponding to the gateway `192.168.98.1` appeared in the ARP table again.

### Evidence — Step 6

**Caption to include before the screenshot:**

> Screenshot of Activity 11.01: the Kali Linux ARP table after accessing Google, showing the reappearance of the `192.168.98.1` entry and its associated MAC address on the `eth0` interface.

[View Evidence — Classes 41–42](../evidencias.pdf)

**Observation:** In this environment, `192.168.98.1` acts as the network gateway. To reach external destinations, traffic must be forwarded through this gateway, making its Layer 2 address association available again.

## 7. Closing the Activity

After recording the evidence, Mozilla Firefox and the Terminal were closed.

## Key Concepts

- **ARP (Address Resolution Protocol):** A protocol used to discover the MAC address associated with an IPv4 address on a local network.
- **ARP table:** Stores IP-to-MAC address mappings known to the system.
- **MAC address:** An address used for communication at the link layer.
- **Gateway:** A device used to forward traffic destined for other networks.
- **`arp -a`:** Displays available ARP entries.
- **`ip neigh`:** Allows users to inspect and manage the Linux neighbor table.

## Activity Workflow

```text
Display the ARP table
        ↓
Clear existing entries
        ↓
Check the table again
        ↓
Access Google
        ↓
Run arp -a
        ↓
Observe the new association
```

## Result

The ARP table was inspected and then cleared. After further network communication, the association for the gateway `192.168.98.1` appeared again, demonstrating that neighbor information can be learned again as network traffic flows.

---

[Back to Classes 41–42](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
