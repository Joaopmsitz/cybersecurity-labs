# Activity 11.02 — Network Interface Aliases on Kali Linux

## Objective

Configure IP address aliases on the `eth0` network interface in Kali Linux by assigning the addresses `192.168.98.41` and `192.168.98.42` to the same physical interface, then validate connectivity using ICMP and SSH.

## Environment

- **Operating system:** Kali GNU/Linux
- **Access:** RDP
- **Network interface:** `eth0`
- **Primary IP address:** `192.168.98.40/24`
- **Aliases:** `192.168.98.41/24` and `192.168.98.42/24`

## 1. Accessing Kali Linux

The Kali Linux machine was accessed via RDP, and the Terminal was opened.

Administrative privileges were obtained using:

```bash
sudo -i
```

## 2. Editing the Network Configuration

The network interface configuration file was opened using:

```bash
nano /etc/network/interfaces
```

The following configurations were added for the two aliases:

```text
auto eth0:1
iface eth0:1 inet static
    address 192.168.98.41
    netmask 255.255.255.0

auto eth0:2
iface eth0:2 inet static
    address 192.168.98.42
    netmask 255.255.255.0
```

This configuration defines two logical interfaces associated with the `eth0` interface.

- `eth0:1` → `192.168.98.41/24`
- `eth0:2` → `192.168.98.42/24`

After entering the configurations, the file was saved using:

```text
Ctrl + X
S
ENTER
```

## 3. Restarting the System

To apply the configuration, Kali Linux was restarted:

```bash
reboot
```

The necessary time was allowed for the machine to become available again.

## 4. Reconnecting to Kali Linux

After the restart, the RDP connection was established again.

Administrative access was restored using:

```bash
sudo -i
```

## 5. Verifying the Interface Addresses

The configuration of the `eth0` interface was checked using:

```bash
ip addr show eth0
```

The output was:

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 12:4d:70:f0:ab:8b brd ff:ff:ff:ff:ff:ff
    inet 192.168.98.40/24 brd 192.168.98.255 scope global dynamic eth0
       valid_lft 3447sec preferred_lft 3447sec
    inet 192.168.98.41/24 brd 192.168.98.255 scope global secondary eth0:1
       valid_lft forever preferred_lft forever
    inet 192.168.98.42/24 brd 192.168.98.255 scope global secondary eth0:2
       valid_lft forever preferred_lft forever
    inet6 fe80::104d:70ff:fef0:ab8b/64 scope link proto kernel_ll
       valid_lft forever preferred_lft forever
```

The output confirms that both new IP addresses were associated with the interface.

### Configured Addresses

| Interface | Address |
|---|---|
| `eth0` | `192.168.98.40/24` |
| `eth0:1` | `192.168.98.41/24` |
| `eth0:2` | `192.168.98.42/24` |

The aliases appear as secondary addresses on the `eth0` interface.

The output also shows:

- **`BROADCAST,MULTICAST,UP,LOWER_UP`:** Interface capabilities and operational state.
- **`mtu 9001`:** Maximum Transmission Unit configured for the interface.
- **`link/ether`:** MAC address of the interface.
- **`scope global`:** IPv4 address scope for network communication.
- **`scope link`:** IPv6 address used within the local link scope.

## 6. Testing the First Alias

The address `192.168.98.41` was tested using:

```bash
ping 192.168.98.41
```

Result:

```text
PING 192.168.98.41 (192.168.98.41) 56(84) bytes of data.
64 bytes from 192.168.98.41: icmp_seq=1 ttl=64 time=0.045 ms
64 bytes from 192.168.98.41: icmp_seq=2 ttl=64 time=0.044 ms
^C
--- 192.168.98.41 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1024ms
rtt min/avg/max/mdev = 0.044/0.044/0.045/0.000 ms
```

Both packets received responses, with **0% packet loss**.

## 7. Testing the Second Alias

The second address was tested using:

```bash
ping 192.168.98.42
```

Result:

```text
PING 192.168.98.42 (192.168.98.42) 56(84) bytes of data.
64 bytes from 192.168.98.42: icmp_seq=1 ttl=64 time=0.038 ms
64 bytes from 192.168.98.42: icmp_seq=2 ttl=64 time=0.044 ms
^C
--- 192.168.98.42 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 0.038/0.041/0.044/0.003 ms
```

Again, both packets received responses, with **0% packet loss**.

## 8. Testing SSH Through the Second Alias

An SSH connection was established using the address `192.168.98.42`:

```bash
ssh aluno@192.168.98.42
```

During the first connection, the host key confirmation prompt was displayed:

```text
The authenticity of host '192.168.98.42 (192.168.98.42)' can't be established.
ED25519 key fingerprint is SHA256:hsrbT/3IfQ22bAUQPUE8T3dpJA/aBVyt3wcyb6zKgO0.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.98.42' (ED25519) to the list of known hosts.
aluno@192.168.98.42's password:
Linux kali 6.6.9-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.6.9-1kali1 (2024-01-08) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the
extent permitted by applicable law.
┏━(Message from Kali developers)
┃ This is a minimal installation of Kali Linux, you likely
┃ want to install supplementary tools. Learn how:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-minimum-setup/
┃ This is a cloud installation of Kali Linux. Learn more about
┃ the specificities of the various cloud images:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-cloud-setup/
┗━(Run: “touch ~/.hushlogin” to hide this message)
┌──(aluno㉿kali)-[~]
└─$ exit
sair
Connection to 192.168.98.42 closed.
```

The connection was successfully established using the second IP address configured as an alias.

### Evidence — Step 8

**Caption to include before the screenshot:**

> Screenshot of Activity 11.02: a successful SSH connection using the address `192.168.98.42`, demonstrating that the alias configured on the `eth0` interface can be used to access the SSH service.

[View Evidence — Classes 41–42](../evidencias.pdf)

## 9. Removing the Aliases

After validation, the configuration file was opened again:

```bash
nano /etc/network/interfaces
```

The previously added configurations were removed:

```text
auto eth0:1
iface eth0:1 inet static
    address 192.168.98.41
    netmask 255.255.255.0

auto eth0:2
iface eth0:2 inet static
    address 192.168.98.42
    netmask 255.255.255.0
```

The file was saved using:

```text
Ctrl + X
S
ENTER
```

## 10. Restarting the System Again

To apply the removal of the aliases, the following command was executed:

```bash
reboot
```

After the restart, the configuration returned to its previous state without the two additional addresses.

## Key Concepts

- **Interface alias:** Allows multiple IP addresses to be associated with the same network interface.
- **`eth0:1` and `eth0:2`:** Identifiers used in this lab to represent aliases of the `eth0` interface.
- **Secondary IP address:** An additional address configured on the same physical interface.
- **ICMP:** A protocol used by `ping` to test connectivity.
- **SSH:** A protocol used for secure remote access to another system.
- **`ip addr`:** A command used to display interface addresses and configuration details.

## Activity Workflow

```text
Edit /etc/network/interfaces
          ↓
Add 192.168.98.41
Add 192.168.98.42
          ↓
Restart Kali Linux
          ↓
Verify with ip addr
          ↓
Test with ping
          ↓
Test SSH
          ↓
Remove the aliases
          ↓
Restart the system
```

## Result

Two secondary IP addresses were configured on the `eth0` interface. Both `192.168.98.41` and `192.168.98.42` responded successfully to ICMP tests, and the second alias was also used successfully to establish an SSH connection.

---

[Back to Classes 41–42](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
