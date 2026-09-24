# Lab 04 — Basic Connectivity Implementation

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/f4ae5189-4ed2-41a2-8b5a-500cacaa8258" />

## Overview

This Packet Tracer lab introduced basic network connectivity by combining switch configuration, end-device IP addressing, and switch management interfaces.

The lab involved configuring two Cisco switches and two PCs, assigning IP addresses to the devices, configuring VLAN 1 as the management interface, and verifying connectivity using IOS `show` commands and `ping`.

## Objectives

* Perform basic configuration on S1 and S2
* Configure console and privileged EXEC passwords
* Configure MOTD banners
* Save switch configurations to NVRAM
* Configure IP addresses on PC1 and PC2
* Configure management IP addresses on S1 and S2
* Verify switch interface status and IP addressing
* Test connectivity using `ping`

---

## Lab Environment

### Network Devices

* Cisco Catalyst 2960 — S1
* Cisco Catalyst 2960 — S2

### End Devices

* PC1
* PC2

### Network Topology

```text id="0h8g5s"
PC1 ───── S1 ───── S2 ───── PC2
```

---

## IP Addressing

| Device | Interface | IP Address      | Subnet Mask     |
| ------ | --------- | --------------- | --------------- |
| S1     | VLAN 1    | `192.168.1.253` | `255.255.255.0` |
| S2     | VLAN 1    | `192.168.1.254` | `255.255.255.0` |
| PC1    | NIC       | `192.168.1.1`   | `255.255.255.0` |
| PC2    | NIC       | `192.168.1.2`   | `255.255.255.0` |

---

# Part 1 — Basic Switch Configuration

The initial configuration was performed on both S1 and S2.

## Configure Hostnames

S1 was configured with the hostname:

```text id="7c5j3v"
S1
```

S2 was configured with the hostname:

```text id="9qj4wk"
S2
```

The hostname was configured from Global Configuration mode:

```text id="f0f3e4"
Switch(config)# hostname S1
```

The same procedure was repeated for S2.

---

## Configure Console and Privileged EXEC Passwords

Console access was protected using:

```text id="f1h5kr"
cisco
```

The privileged EXEC password was configured as:

```text id="3r7x9a"
class
```

The console configuration used:

```text id="v6q7bx"
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
```

The privileged EXEC password was configured using:

```text id="p0h5zc"
S1(config)# enable secret class
```

The same configuration was applied to S2.

---

## Verify Password Configuration

The password configuration was verified using:

```text id="s7s9k1"
S1# show running-config
```

The console and privileged EXEC authentication settings were checked in the running configuration.

---

## Configure MOTD Banner

A security warning was configured using the `banner motd` command:

```text id="2w6v0g"
S1(config)# banner motd "Authorized Access Only!"
```

The same type of banner was configured on S2.

The MOTD banner provides a warning to users attempting to access the device and can communicate that unauthorized access is prohibited.

---

## Save Configuration

The completed switch configurations were saved to NVRAM:

```text id="r6q0ae"
S1# copy running-config startup-config
```

The same command was executed on S2.

---

# Part 2 — Configure PCs

## PC1 Configuration

PC1 was configured with:

```text id="m3w4pg"
IP Address:    192.168.1.1
Subnet Mask:   255.255.255.0
```

## PC2 Configuration

PC2 was configured with:

```text id="f1n4z8"
IP Address:    192.168.1.2
Subnet Mask:   255.255.255.0
```

Both PCs were placed in the same IPv4 subnet.

---

## Initial Connectivity Test

Connectivity from PC1 to S1 was tested using:

```text id="8p3r7x"
PC> ping 192.168.1.253
```

The ping test was used to determine whether basic IP connectivity to the switch management interface was available.

---

# Part 3 — Configure the Switch Management Interface

## Why Does a Switch Need an IP Address?

A Layer 2 switch can forward Ethernet frames using MAC addresses without having an IP address.

However, an IP address can be assigned to a switch management interface so administrators can remotely manage and monitor the device using protocols such as SSH.

---

## Configure S1 Management Interface

The VLAN 1 interface was configured as the management interface:

```text id="4q1v0c"
S1# configure terminal
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.253 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
```

### Why Use `no shutdown`?

The `no shutdown` command administratively enables the interface.

Without it, the VLAN interface may remain administratively down even when its configuration is correct.

---

## Configure S2 Management Interface

S2 was configured using its assigned management IP address:

```text id="x4b2k9q"
S2# configure terminal
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.1.254 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
```

---

## Verify IP Configuration

The management interfaces were verified using:

```text id="g7f5q2"
S1# show ip interface brief
```

The same command was used on S2:

```text id="n8k3p1"
S2# show ip interface brief
```

The command provides a quick overview of:

* Interface names
* IP addresses
* Administrative status
* Line protocol status

The running configuration can also be inspected with:

```text id="v9r2m6"
S1# show running-config
```

---

## Save Configuration to NVRAM

After configuring the management interfaces, the changes were saved:

```text id="c4h8x1"
S1# copy running-config startup-config
S2# copy running-config startup-config
```

This ensures the configuration persists after a reboot.

---

# Connectivity Verification

Connectivity was tested using ICMP `ping`.

### PC1 → PC2

```text id="z5v3n8"
PC> ping 192.168.1.2
```

### PC1 → S1

```text id="j7c2m4"
PC> ping 192.168.1.253
```

### PC1 → S2

```text id="k6p9r3"
PC> ping 192.168.1.254
```

All required connectivity tests were expected to succeed.

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/7bf9f6c4-935c-4456-b39e-a98ad2436113" />

---

## Key Commands

| Purpose                        | Command                              |
| ------------------------------ | ------------------------------------ |
| Enter Privileged EXEC          | `enable`                             |
| Enter Global Configuration     | `configure terminal`                 |
| Configure hostname             | `hostname S1`                        |
| Configure console line         | `line console 0`                     |
| Configure console password     | `password cisco`                     |
| Require console authentication | `login`                              |
| Configure privileged password  | `enable secret class`                |
| Configure MOTD                 | `banner motd "message"`              |
| Enter VLAN interface           | `interface vlan 1`                   |
| Configure IP address           | `ip address <ip> <mask>`             |
| Enable interface               | `no shutdown`                        |
| Verify interfaces              | `show ip interface brief`            |
| View running configuration     | `show running-config`                |
| Save configuration             | `copy running-config startup-config` |
| Test connectivity              | `ping <ip>`                          |

