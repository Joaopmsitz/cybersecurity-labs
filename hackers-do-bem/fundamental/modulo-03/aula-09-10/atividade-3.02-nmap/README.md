# Activity 3.02 — Network Scanning with Nmap

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 09–10  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use Nmap to discover hosts, identify active devices on a network, analyze port states, filter scan results, and observe the packets used during scanning.

The activity was conducted in a controlled laboratory environment using the `192.168.98.0/24` network.

## Environment

- **Operating system:** Kali Linux
- **Tool:** Nmap 7.95
- **Network interface:** `eth0`
- **Laboratory network:** `192.168.98.0/24`
- **Kali Linux IP address:** `192.168.98.40/24`

## Procedure

### 1. Obtain Root Access

A terminal was opened and an administrative session was started:

```bash
sudo -i
```

This command provided a root shell for the laboratory procedures.

### 2. Identify Network Interfaces

The `ifconfig` command was used to inspect the available network interfaces and IP addresses:

```bash
ifconfig
```

**Observed output:**

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0
        ether 02:42:8e:9c:ad:13  txqueuelen 0  (Ethernet)

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0
        inet6 fe80::a00:27ff:fe4e:66a1  prefixlen 64  scopeid 0x20<link>
        ether 0a:00:27:4e:66:a1  txqueuelen 1000  (Ethernet)

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
```

The interface used to access the laboratory network was `eth0`, with the address `192.168.98.40/24`.

The output also showed the `docker0` interface, associated with a Docker network, and the loopback interface `lo`.

### 3. Discover Hosts with Nmap

To identify active hosts on the network, the following command was used:

```bash
nmap -sn 192.168.98.0/24
```

The `-sn` option performs host discovery without the conventional port scan.

**Observed output:**

```text
Starting Nmap 7.95 ( https://nmap.org )
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
Host is up.

Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
Host is up.

Nmap scan report for ip-192-168-98-20.ec2.internal (192.168.98.20)
Host is up.

Nmap scan report for ip-192-168-98-30.ec2.internal (192.168.98.30)
Host is up.

Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
Host is up.

Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
Host is up.

Nmap done: 256 IP addresses (6 hosts up) scanned in ...
```

Six active hosts were identified in the laboratory network:

- `192.168.98.1`
- `192.168.98.2`
- `192.168.98.20`
- `192.168.98.30`
- `192.168.98.201`
- `192.168.98.40`

The results represent the hosts reported as active during this scan. Host discovery results may vary depending on network configuration, filtering, and device availability.

### 4. Filter the Discovered IP Addresses

A directory was selected to store the results:

```bash
cd /home/aluno/Documentos/
```

The directory contents were checked:

```bash
ls
```

The Nmap results were then filtered using a command pipeline:

```bash
nmap -sn 192.168.98.0/24 | grep 192 | cut -d ' ' -f 5 > ips.txt
```

The command combines several shell operations:

- `nmap -sn` — discovers active hosts.
- `grep 192` — filters lines containing the string `192`.
- `cut -d ' ' -f 5` — extracts the fifth field when splitting on individual space characters.
- `>` — redirects command output into a file.
- `ips.txt` — the file used to store the results.

The file was checked after creation:

```bash
ls
```

Its contents were displayed with:

```bash
cat ips.txt
```

**Observed result:**

```text
192.168.98.1
192.168.98.2
192.168.98.20
192.168.98.30
192.168.98.201
192.168.98.40
```

This step demonstrates the use of pipes (`|`) and output redirection (`>`) to transform the output of one tool into input for other system utilities.

**Technical note:** Using `cut -d ' ' -f 5` with Nmap's formatted output can be fragile because spacing and output formats may vary. The observed result above is preserved as recorded in the laboratory. For more robust automation, structured output or explicit extraction of IP addresses is preferable.

### 5. Perform an ACK Scan

The `-sA` option was used:

```bash
nmap -sA 192.168.98.0/24
```

A TCP ACK scan is primarily used to investigate whether ports are filtered by a firewall. Unlike a SYN scan, it should not be interpreted as a direct method for identifying open ports.

This scan can report states such as:

- **filtered** — filtering by a firewall or another network mechanism prevents Nmap from determining whether the port is reachable.
- **unfiltered** — the probe can reach the port, but the ACK scan cannot determine whether the port is open or closed.

The results depend on the responses received and the network's filtering behavior.

### 6. Display Port Scan Results

The following command was used for another scan:

```bash
nmap --open 192.168.98.0/24
```

**Observed output:**

```text
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
All 1000 scanned ports on 192.168.98.1 are filtered

Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
PORT   STATE       SERVICE
53/tcp unfiltered  domain
999/tcp filtered   ...

Nmap scan report for ip-192-168-98.20.ec2.internal (192.168.98.20)
All 1000 scanned ports on 192.168.98.20 are filtered

Nmap scan report for ip-192-168-98.30.ec2.internal (192.168.98.30)
All 1000 scanned ports on 192.168.98.30 are filtered

Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
All 1000 scanned ports on 192.168.98.201 are unfiltered

Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
All 1000 scanned ports on 192.168.98.40 are unfiltered

Nmap done: 256 IP addresses (6 hosts up) scanned in 12.73 seconds
```

An important observation is that **`unfiltered` does not mean `open`**. Port states must be interpreted in the context of the scan type used.

The ACK scan is primarily designed to investigate packet filtering, and an `unfiltered` result does not establish that a service is listening on that port.

The `--open` option is intended to limit reported ports to those considered open or potentially open by Nmap. Since the captured output also contains `filtered` and `unfiltered` states, these lines have been retained exactly as provided in the laboratory record. They should not be treated as proof that those ports are open.

### 7. Observe Packets with `--packet-trace`

Finally, the `--packet-trace` option was used to display information about packets involved in the scan:

```bash
nmap --packet-trace 192.168.98.0/24
```

Among the observations were ARP requests used for host discovery, for example:

```text
ARP who-has 192.168.98.x tell 192.168.98.40
```

The scan also identified open ports on the laboratory host itself:

```text
22/tcp open  ssh
3389/tcp open  ms-wbt-server
```

The `--packet-trace` option provides additional visibility into the scanning process, making it possible to relate Nmap's reported results to the packets used for host discovery and analysis.

Port `22/tcp` was identified as associated with SSH, while `3389/tcp` was identified as associated with Microsoft's Remote Desktop Protocol (RDP).

These results apply to the observed laboratory environment and do not establish that the same ports will be open in other environments.

### 8. Remove the Temporary File

After completing the activity, the file used to store the IP addresses was removed:

```bash
rm ips.txt
```

This command deletes the temporary file `ips.txt` from the current directory.

## Commands Used

The commands used throughout the activity were:

```bash
sudo -i
ifconfig
nmap -sn 192.168.98.0/24
cd /home/aluno/Documentos/
ls
nmap -sn 192.168.98.0/24 | grep 192 | cut -d ' ' -f 5 > ips.txt
cat ips.txt
nmap -sA 192.168.98.0/24
nmap --open 192.168.98.0/24
nmap --packet-trace 192.168.98.0/24
rm ips.txt
```

## Concepts Practiced

### Nmap

A network scanning tool used for host discovery, port analysis, and identification of network characteristics.

### Host Discovery

The process of identifying which IP addresses appear to be active within a network segment.

### TCP ACK Scan

The `-sA` option sends TCP ACK probes and is primarily used to examine packet filtering and firewall behavior.

### Port States

The activity covered states such as `filtered` and `unfiltered`. Their interpretation depends on the type of scan performed and the responses received.

### `--open`

An option intended to limit the reported results to ports that Nmap considers open or potentially open. It does not make every reported state equivalent to `open`.

### `--packet-trace`

Displays information about packets used during Nmap execution, providing additional visibility into the scanning process.

### Pipes and Output Redirection

The activity also used basic shell features:

- `|` to chain commands and pass output between utilities.
- `>` to redirect output into a file.

These techniques are useful for extracting, processing, and storing information from command-line security tools.

## Results

The activity provided practical experience using Nmap on a laboratory network through several stages:

- Identifying the network interface and the machine's IP address.
- Discovering active hosts.
- Extracting discovered IP addresses using Linux commands.
- Investigating packet filtering with an ACK scan.
- Reviewing port scan results.
- Observing packets used during scanning.

The exercise reinforced the relationship between host discovery, port analysis, network filtering, firewalls, and TCP/IP traffic.

The results also highlighted the importance of interpreting Nmap port states according to the scan method rather than assuming that every reachable or unfiltered port is open.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 09–10.

**Recorded screenshot:** Step 6 of the activity, as required by the laboratory instructions.

[View Evidence — Classes 09–10](../evidencias.pdf)

---

[Back to Classes 09–10](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
