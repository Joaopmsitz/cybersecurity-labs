# Activity 11.04 — QoS on Kali Linux

## Objective

Explore Quality of Service (QoS) mechanisms on Linux using the `tc` (Traffic Control) command to create queues and filters for controlling traffic on the `eth0` interface, and subsequently apply a transmission rate limit.

## Environment

- **Operating system:** Kali GNU/Linux
- **Network interface:** `eth0`
- **Tool:** `tc` (Traffic Control)
- **Gateway:** `192.168.98.1`
- **Machine IP address:** `192.168.98.40`

## 1. Accessing Kali Linux

The Kali Linux machine was accessed, and the Terminal was opened.

Administrative privileges were obtained using:

```bash
sudo -i
```

## 2. Checking the Network Interface

The network interface configuration was checked using:

```bash
ifconfig
```

The main interface used in this activity was `eth0`.

The observed information included:

```text
eth0: ...
      inet 192.168.98.40
      netmask 255.255.255.0
      mtu 9001
```

The `eth0` interface has the IP address `192.168.98.40` and is connected to the network used in the lab.

## 3. Creating a Priority Queue

A priority queueing discipline (`qdisc`) of type `prio` was added to the `eth0` interface:

```bash
tc qdisc add dev eth0 root handle 1: prio
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip protocol 1 0xff flowid 1:1
```

The first command creates a priority queue:

```bash
tc qdisc add dev eth0 root handle 1: prio
```

### Main Parameters

- **`tc`:** Linux traffic control utility.
- **`qdisc`:** Queueing discipline responsible for managing packet queues.
- **`add`:** Adds a new configuration.
- **`dev eth0`:** Applies the configuration to the `eth0` interface.
- **`root`:** Sets the queueing discipline as the interface's root discipline.
- **`handle 1:`:** Identifies the queueing discipline.
- **`prio`:** Uses a priority-based queueing discipline.

The second command adds a filter:

```bash
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip protocol 1 0xff flowid 1:1
```

In this case, the filter uses the IP protocol and matches protocol number `1`, which corresponds to ICMP, directing the matching packets to class `1:1`.

## 4. Removing the Previous QDisc

Since Linux allows only one root queueing discipline per interface, the previous configuration was removed:

```bash
tc qdisc del dev eth0 root
```

This command removes the root QDisc previously configured on the `eth0` interface.

## 5. Testing Connectivity to the Gateway

Before configuring a new QoS policy, connectivity to the gateway was tested:

```bash
ping 192.168.98.1
```

Result:

```text
PING 192.168.98.1 (192.168.98.1) 56(84) bytes of data.
64 bytes from 192.168.98.1: icmp_seq=1 ttl=255 time=0.325 ms
64 bytes from 192.168.98.1: icmp_seq=2 ttl=255 time=0.424 ms
64 bytes from 192.168.98.1: icmp_seq=3 ttl=255 time=0.450 ms
^C
--- 192.168.98.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2040ms
rtt min/avg/max/mdev = 0.325/0.399/0.450/0.053 ms
```

The test results showed:

- **Packets transmitted:** 3
- **Packets received:** 3
- **Packet loss:** 0%
- **Average response time:** Approximately 0.399 ms

## 6. Creating an HTB QDisc

A Hierarchical Token Bucket (HTB) queueing discipline was configured:

```bash
tc qdisc add dev eth0 root handle 1: htb
tc class add dev eth0 parent 1: classid 1:1 htb rate 10mbit
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip src 192.168.98.1 flowid 1:1
```

The first line creates the HTB QDisc:

```bash
tc qdisc add dev eth0 root handle 1: htb
```

The second line creates a class with a rate limit:

```bash
tc class add dev eth0 parent 1: classid 1:1 htb rate 10mbit
```

In this case, class `1:1` was configured with a rate of:

```text
10 Mbit/s
```

Finally, a filter was created to match traffic whose source IP address is `192.168.98.1`:

```bash
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip src 192.168.98.1 flowid 1:1
```

Matching traffic is therefore directed to class `1:1`.

## 7. Removing the HTB Configuration

Before performing the final test, the existing QDisc was removed again:

```bash
tc qdisc del dev eth0 root
```

This allowed a new traffic control configuration to be applied to the interface.

## 8. Limiting the Interface to 1 Mbit/s

To demonstrate direct transmission rate control, a Token Bucket Filter (TBF) QDisc was configured:

```bash
tc qdisc add dev eth0 root tbf rate 1mbit burst 10kb latency 50ms
```

The configuration uses the following parameters:

- **`tbf`:** Token Bucket Filter.
- **`rate 1mbit`:** Sets the rate limit to 1 Mbit/s.
- **`burst 10kb`:** Sets the permitted burst size.
- **`latency 50ms`:** Sets the maximum latency parameter used for queue management.

With this configuration, traffic on the interface is subject to the rate limit imposed by the QDisc.

### Evidence — Step 8

**Caption to include before the screenshot:**

> Screenshot of Activity 11.04: the TBF QDisc configuration on the `eth0` interface, using `rate 1mbit`, `burst 10kb`, and `latency 50ms` to limit the interface's transmission rate.

[View Evidence — Classes 41–42](../evidencias.pdf)

## 9. Removing the Rate Limit

After recording the evidence, the QoS configuration was removed:

```bash
tc qdisc del dev eth0 root
```

This removed the 1 Mbit/s limit previously applied to the interface.

## 10. Closing the Activity

After removing the QoS configuration, the Terminal was closed.

## Key Concepts

- **QoS (Quality of Service):** A set of mechanisms used to control and organize network traffic.
- **`tc`:** A Linux utility for traffic control and queue management.
- **QDisc:** A queueing discipline that determines how packets are handled by an interface.
- **PRIO:** A priority-based queueing discipline.
- **HTB:** A hierarchical mechanism for controlling traffic rates and classes.
- **TBF:** A Token Bucket-based mechanism used to limit transmission rates.
- **ICMP:** A protocol used by `ping` to test connectivity.

## Activity Workflow

```text
Check the network interface
       ↓
Create a PRIO QDisc
       ↓
Add an ICMP filter
       ↓
Remove the QDisc
       ↓
Test gateway connectivity
       ↓
Create an HTB QDisc
       ↓
Classify traffic
       ↓
Remove the QDisc
       ↓
Apply a 1 Mbit/s TBF limit
       ↓
Remove the configuration
```

## Result

Different traffic control mechanisms were explored using `tc`, including PRIO, HTB, and TBF. In the final test, the `eth0` interface was configured with a maximum rate of 1 Mbit/s, demonstrating the practical use of QoS for bandwidth control.

---

[Back to Classes 41–42](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
