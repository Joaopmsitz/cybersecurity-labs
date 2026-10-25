# Activity 3.06 — Exploring Network Diagnostic Tools on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 11–12  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use commands available in Kali Linux to diagnose network status, identify interfaces, test connectivity, inspect routes, query protocol statistics, and check active network connections and services.

The activity was conducted in a laboratory environment, and the commands were used exclusively for academic purposes.

## Environment

- **Operating system:** Kali Linux
- **Primary network interface:** `eth0`
- **Machine IP address:** `192.168.98.40/24`
- **Network:** `192.168.98.0/24`

## Procedure

### 1. Obtain Superuser Access

The terminal was opened and the following command was executed:

```bash
sudo -i
```

After entering the laboratory environment password, the terminal operated as the root user.

### 2. Identify Network Interfaces

The following command was used:

```bash
ifconfig
```

**Observed output:**

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:df:26:13:80  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::1005:27ff:fe44:1631  prefixlen 64  scopeid 0x20<link>
        ether 12:05:27:44:16:31  txqueuelen 1000  (Ethernet)
        RX packets 1818194  bytes 2694820836 (2.5 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61082  bytes 77348531 (73.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Loopback Local)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Three network interfaces were identified:

- `docker0` — virtual interface used by Docker.
- `eth0` — primary interface connected to the laboratory network.
- `lo` — loopback interface.

The `eth0` interface had the address `192.168.98.40/24`.

The output also displayed traffic counters, interface status flags, the MTU, and the IPv6 link-local address assigned to `eth0`.

### 3. Test Connectivity with Ping

To test connectivity and verify domain name resolution, the following command was used:

```bash
ping www.google.com
```

**Observed output:**

```text
PING www.google.com (172.253.63.106) 56(84) bytes of data.
64 bytes from bi-in-f106.1e100.net (172.253.63.106): icmp_seq=1 ttl=109 time=1.42 ms
64 bytes from bi-in-f106.1e100.net (172.253.63.106): icmp_seq=2 ttl=109 time=1.41 ms
```

Execution was interrupted using:

```text
Ctrl + C
```

The result shows that `www.google.com` resolved to `172.253.63.106` at the time of the test and that responses were received for the transmitted ICMP echo requests.

The main fields observed were:

- `icmp_seq` — sequence number of the packet.
- `ttl` — Time To Live value observed in the response.
- `time` — round-trip time (RTT) of the communication.

Ping provides a basic way to test reachability, although a lack of responses does not always mean a host is unavailable. ICMP traffic can be filtered by network devices or the destination host.

### 4. Trace the Route with Traceroute

The following command was executed:

```bash
traceroute -I grancursos.com.br
```

The `-I` option makes traceroute use ICMP probes.

**Output recorded in the laboratory instructions:**

```text
traceroute to grancursos.com.br (172.67.175.92), 30 hops max, 60 byte packets
 1  244.5.7.59 (244.5.7.59)  2.953 ms  2.920 ms *
 2  240.4.116.42 (240.4.116.42)  0.305 ms  0.299 ms  0.318 ms
 3  242.12.75.131 (242.12.75.131)  1.596 ms  1.589 ms  1.584 ms
 4  240.3.180.12 (240.3.180.12)  1.048 ms  1.332 ms  1.557 ms
 5  240.3.180.29 (240.3.180.29)  0.636 ms  0.961 ms  0.955 ms
 6  99.83.116.94 (99.83.116.94)  0.949 ms  1.081 ms  1.101 ms
 7  * * *
 8  173.245.63.137 (173.245.63.137)  1.421 ms  1.404 ms  1.359 ms
 9  172.67.175.92 (172.67.175.92)  0.901 ms  0.889 ms  0.870 ms
```

Traceroute helps visualize the hops traversed by probes between the source and destination.

The `*` symbols represent probes that did not receive a response within the expected time. This does not necessarily indicate a connectivity failure: routers and intermediate devices may not respond to particular ICMP probes.

The output also illustrates how a network path can traverse different networks and infrastructure before reaching its destination.

**Observation:** Traceroute results may vary depending on the time of execution, routing decisions, load balancing, and filtering policies. The addresses shown above are preserved from the laboratory record and should not be interpreted as a current route.

### 5. Inspect Interface Statistics with `netstat -i`

The following command was used:

```bash
netstat -i
```

**Observed output:**

```text
Tabela de Interfaces do Kernel
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
docker0          1500        0      0      0 0             0      0      0      0 BMU
eth0             9001     8055      0      0 0          9143      0      0      0 BMRU
lo              65536       23      0      0 0            23      0      0      0 LRU
```

The command displays statistics associated with network interfaces.

Important fields include:

- `Iface` — interface name.
- `MTU` — Maximum Transmission Unit.
- `RX-OK` — packets received successfully.
- `RX-ERR` — receive errors.
- `RX-DRP` — received packets dropped.
- `RX-OVR` — receive overrun events.
- `TX-OK` — packets transmitted successfully.
- `TX-ERR` — transmission errors.
- `TX-DRP` — packets dropped during transmission.
- `TX-OVR` — transmission overrun events.
- `Flg` — flags associated with the interface.

The captured output shows no receive or transmission errors for the listed interfaces in those counters.

**Technical note:** The packet counters reported by this command differ from those shown earlier by `ifconfig`. These values are retained as recorded in the lab. When comparing counters from different commands, consider whether they were collected at different times or through different system reporting mechanisms.

### 6. Inspect the Routing Table

The following command was executed:

```bash
netstat -rn
```

**Observed output:**

```text
Tabela de Roteamento IP do Kernel
Destino         Roteador        MáscaraGen.    Opções   MSS Janela  irtt Iface
0.0.0.0         192.168.98.1    0.0.0.0         UG        0 0          0 eth0
172.17.0.0      0.0.0.0         255.255.0.0     U         0 0          0 docker0
192.168.98.0    0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

The table displays the routes known to the system.

The entry:

```text
0.0.0.0         192.168.98.1    0.0.0.0         UG
```

represents the default route, using `192.168.98.1` as the gateway through the `eth0` interface.

The network:

```text
192.168.98.0/24
```

is directly associated with `eth0`.

The network:

```text
172.17.0.0/16
```

is associated with the virtual `docker0` interface.

The `-r` option displays the routing table, while `-n` prevents address and port resolution so that addresses are shown numerically.

### 7. Inspect Network Protocol Statistics

The following command was used:

```bash
netstat -s
```

**Observed output:**

```text
Ip:
    Forwarding: 1
    9136 total packets received
    4 with invalid addresses
    0 forwarded
    0 incoming packets discarded
    9132 incoming packets delivered
    10381 requests sent out
Icmp:
    29 ICMP messages received
    0 input ICMP message failed
    Histograma de entrada ICMP:
        destination unreachable: 3
        timeout in transit: 15
        echo replies: 11
    56 ICMP messages sent
    0 ICMP messages failed
    Histograma de saída ICMP
        destination unreachable: 3
        echo requests: 53
IcmpMsg:
        InType0: 11
        InType3: 3
        InType11: 15
        OutType3: 3
        OutType8: 53
Tcp:
    68 active connection openings
    3 passive connection openings
    0 failed connection attempts
    1 connection resets received
    1 connections established
    9068 segments received
    16104 segments sent out
    0 segments retransmitted
    0 bad segments received
    0 resets sent
Udp:
    43 packets received
    3 packets to unknown port received
    0 packet receive errors
    48 packets sent
    0 receive buffer errors
    0 send buffer errors
UdpLite:
TcpExt:
    67 TCP sockets finished time wait in fast timer
    204 delayed acks sent
    2 packet headers predicted
    1628 acknowledgments not containing data payload received
    6007 predicted acknowledgments
    TCPBacklogCoalesce: 2
    TCPRcvCoalesce: 11
    TCPAutoCorking: 43
    TCPOrigDataSent: 14843
    TCPHystartTrainDetect: 1
    TCPHystartTrainCwnd: 16
    TCPDelivered: 14910
IpExt:
    OutMcastPkts: 10
    InOctets: 535228
    OutOctets: 70865774
    OutMcastOctets: 1590
    InNoECTPkts: 9172
    InECT0Pkts: 2
MPTcpExt:
```

The output presents statistics grouped by protocol and extension.

#### IP

Displays general information about IP traffic, including packets received, discarded, and sent.

#### ICMP

Displays statistics for ICMP messages, including:

- Echo requests.
- Echo replies.
- Destination unreachable messages.
- Time exceeded messages.

#### TCP

Displays statistics related to TCP connections, including connection openings, segments received and sent, retransmissions, and resets.

#### UDP

Displays statistics for UDP datagrams received and sent.

#### TcpExt and IpExt

Provide additional statistics related to TCP and IP operation.

These counters reflect activity during the lifetime of the system or network stack, depending on the counter. They are not limited to the individual commands executed during this exercise.

### 8. Inspect Network Connections and Services

The final step, which was also the main evidence requested for the activity, used:

```bash
netstat -anptu
```

The command combines several options:

- `-a` — displays all connections and listening sockets.
- `-n` — displays addresses and ports numerically.
- `-p` — shows the associated process ID and program when available.
- `-t` — includes TCP connections.
- `-u` — includes UDP sockets.

**Observed output:**

```text
Conexões Internet Ativas (servidores e estabelecidas)
Proto Recv-Q Send-Q Endereço Local          Endereço Remoto         Estado      PID/Program name
tcp        0      0 127.0.0.1:36367         0.0.0.0:*               OUÇA       576/containerd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               OUÇA       618/sshd: /usr/sbin
tcp6       0      0 :::22                   :::*                    OUÇA       618/sshd: /usr/sbin
tcp6       0      0 :::3389                 :::*                    OUÇA       641/xrdp
tcp6       0      0 ::1:3350                :::*                    OUÇA       581/xrdp-sesman
tcp6       0      0 192.168.98.40:3389      192.168.98.201:49732    ESTABELECIDA 2206/xrdp
udp        0      0 0.0.0.0:68              0.0.0.0:*                           441/dhclient
udp6       0      0 fe80::1005:27ff:fe4:546 :::*                                494/dhclient
```

The output allows network ports, connection states, and running processes to be examined together.

For example:

```text
tcp  0  0  0.0.0.0:22  0.0.0.0:*  OUÇA  618/sshd
```

indicates that the `sshd` service was listening on TCP port `22`.

An RDP connection was also observed:

```text
tcp6  0  0  192.168.98.40:3389  192.168.98.201:49732  ESTABELECIDA  2206/xrdp
```

In this case, port `3389` was associated with the `xrdp` service, and an established connection to another address in the laboratory environment was shown.

The output also showed `dhclient` associated with UDP port `68`, which is used by DHCP clients.

The state labels `OUÇA` and `ESTABELECIDA` correspond to listening and established connections, respectively.

**Note:** The command output is preserved as recorded in the laboratory, including the localized labels. Actual process names, ports, and connection states depend on the services running when the command is executed.

### 9. Finish the Activity

After completing the network queries, the terminal was closed.

## Commands Used

The following commands were used throughout the activity:

```bash
sudo -i
ifconfig
ping www.google.com
traceroute -I grancursos.com.br
netstat -i
netstat -rn
netstat -s
netstat -anptu
```

The `ping` process was stopped using `Ctrl + C`.

## Concepts Practiced

The activity used several tools for network diagnostics:

| Command | Purpose |
|---|---|
| `ifconfig` | Identify network interfaces and IP addresses |
| `ping` | Test connectivity using ICMP |
| `traceroute -I` | Observe network hops using ICMP probes |
| `netstat -i` | Inspect network interface statistics |
| `netstat -rn` | Display the routing table |
| `netstat -s` | Inspect protocol statistics |
| `netstat -anptu` | Examine connections, ports, states, and associated processes |

Together, these commands provide a practical overview of the state of a Linux system's network.

## Results

The activity provided experience analyzing several layers of networking in Kali Linux, from interface configuration to active connections and services.

The following information was examined:

- Network interfaces and IP addresses.
- Connectivity through ICMP.
- Network route hops between the source and destination.
- Packet transmission and reception statistics.
- Configured routes.
- IP, ICMP, TCP, and UDP protocol statistics.
- Listening ports.
- Established connections.
- Processes associated with network sockets.

The final `netstat -anptu` step was used as the main evidence for the activity, as specified in the laboratory instructions.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 11–12.

**Recorded screenshot:** The final step using `netstat -anptu`, as specified in the laboratory instructions.

[View Evidence — Classes 11–12](../evidencias.pdf)

---

[Back to Classes 11–12](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
