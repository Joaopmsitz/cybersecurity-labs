# Activity 11.10 — Blocking ICMP Packets from Windows Server 2022 on Kali Linux

## Objective

Use `iptables` on Kali Linux to block ICMP echo-request packets originating from Windows Server 2022, verify the effect of the rule using the `ping` command, and subsequently remove the rule to restore communication.

## Environment

- **Kali Linux:** `192.168.98.40`
- **Windows Server 2022:** `192.168.98.30`
- **Tool:** `iptables`
- **Protocol:** ICMP
- **Blocked ICMP type:** `echo-request`

## 1. Checking the Windows Server 2022 IP Address

Windows Server 2022 was accessed via RDP.

The following command was executed in Command Prompt:

```cmd
ipconfig
```

The displayed output was:

```text
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : ec2.internal
   Link-local IPv6 Address . . . . . : fe80::919a:6c84:9a17:42e3%7
   IPv4 Address. . . . . . . . . . . : 192.168.98.30
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.98.1
```

The IPv4 address of the Windows Server used in the lab is:

```text
192.168.98.30
```

## 2. Accessing Kali Linux

The Windows Server RDP window was minimized, and Kali Linux was accessed using the following address:

```text
192.168.98.40
```

On Kali Linux, the Terminal was opened, and administrative privileges were obtained using:

```bash
sudo -i
```

## 3. Checking Kali Linux Network Interfaces

The following command was executed:

```bash
ifconfig
```

The `eth0` interface displayed the following IPv4 address:

```text
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
```

The `docker0` interface was also present:

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
```

The loopback interface was also available:

```text
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1
```

The address used by Kali Linux on the lab network is:

```text
192.168.98.40
```

## 4. Testing Communication Before Blocking

The following command was executed on Windows Server 2022:

```cmd
ping 192.168.98.40
```

Communication worked normally:

```text
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time=1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
```

This test confirmed that, before the firewall rule was applied, Windows Server could send ICMP requests to Kali Linux and receive the corresponding replies.

The initial traffic flow was:

```text
Windows Server
192.168.98.30
      │
      │ ICMP echo-request
      ▼
Kali Linux
192.168.98.40
      │
      │ ICMP echo-reply
      ▼
Windows Server
```

## 5. Creating the ICMP Blocking Rule

The following rule was created on Kali Linux:

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

The rule applies to ICMP packets received by Kali Linux.

### Parameters Used

#### `iptables`

A tool used to configure packet-filtering rules through Netfilter.

#### `-A INPUT`

Adds a rule to the `INPUT` chain.

The `INPUT` chain processes packets destined for Kali Linux itself.

#### `-p icmp`

Specifies that the rule applies to the following protocol:

```text
ICMP
```

#### `--icmp-type echo-request`

Specifies the type of ICMP message to be blocked:

```text
echo-request
```

This is the message type used by `ping` to request a response from the destination host.

#### `-j DROP`

Defines the action applied to matching packets.

`DROP` discards the packet, preventing it from being processed normally by the system.

Therefore, the rule can be interpreted as follows:

```text
Incoming packet
      ↓
     ICMP
      ↓
echo-request?
      ↓
     YES
      ↓
     DROP
      ↓
Packet discarded
```

> **Important:** This rule does not block the entire ICMP protocol. It specifically matches `echo-request` messages.

## 6. Testing the Blocking Rule

After creating the rule, Windows Server 2022 was used again to execute:

```cmd
ping 192.168.98.40
```

The requests no longer received responses from Kali Linux.

The observed result was:

```text
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.98.40:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

The 100% packet loss demonstrates that the four requests sent by Windows Server did not receive responses.

This occurred because the ICMP echo-request packets were discarded by `iptables` on Kali Linux.

### Evidence — Step 10

**Caption to include before the screenshot:**

> Screenshot of Activity 11.10: the result of `ping 192.168.98.40` executed on Windows Server 2022 after applying the `iptables` rule, showing 100% packet loss and no responses from Kali Linux.

[**View Evidence — Module 11 / Classes 43–44**](../evidencias.pdf)

## 7. Removing the Blocking Rule

After confirming that the blocking rule worked, it was removed on Kali Linux using:

```bash
iptables -D INPUT -p icmp --icmp-type echo-request -j DROP
```

The parameter:

```text
-D
```

removes an existing rule.

The remaining parameters correspond to the rule that was created previously.

## 8. Confirming Communication Again

After removing the rule, the following command was executed again on Windows Server:

```cmd
ping 192.168.98.40
```

Communication was restored:

```text
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time=1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64

Ping statistics for 192.168.98.40:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

The result shows:

```text
Packets: Sent = 4
Received = 4
Lost = 0 (0% loss)
```

Therefore, after removing the rule, ICMP requests started receiving responses normally again.

## 9. Completing the Activity

After confirming that communication was working, the windows used during the lab were closed.

## Key Concepts

- **ICMP:** A protocol used for control and diagnostic messages in IP networks.
- **Echo Request:** An ICMP message used by `ping` to request a response.
- **Echo Reply:** The response corresponding to an echo-request.
- **iptables:** A tool used to configure Netfilter rules.
- **INPUT:** A chain responsible for processing packets destined for the local system.
- **DROP:** An action that discards packets matching a rule.
- **Ping:** A tool used to test connectivity through ICMP messages.

## Activity Workflow

```text
Windows Server
192.168.98.30
      ↓
ping 192.168.98.40
      ↓
Kali responds
      ↓
Create ICMP DROP rule
      ↓
Run ping again
      ↓
100% packet loss
      ↓
Remove the rule
      ↓
Run ping again
      ↓
0% packet loss
```

## Result

An `iptables` rule was created to discard ICMP echo-request packets received by Kali Linux. After applying the rule, Windows Server showed 100% packet loss when executing `ping` against `192.168.98.40`. The rule was subsequently removed, and communication was restored, with 0% packet loss.

---

[Back to Classes 43–44](../README.md) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
