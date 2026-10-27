# Lab 06 — Basic Switch and End Device Configuration — Physical Mode

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/8808515e-1266-41e5-80da-44d7235c6ef9" />

## Overview

This Packet Tracer Physical Mode (PTPM) activity focused on building and configuring a small Ethernet LAN using two Cisco switches and two end devices.

The lab introduced physical topology construction, console connectivity, basic Cisco IOS configuration, IPv4 addressing, interface verification, configuration persistence, and connectivity testing.

Unlike previous labs performed primarily through the logical workspace, this activity required physically connecting the devices and selecting the appropriate switch ports and cables.

---

## Objectives

* Build a small Ethernet network in Packet Tracer Physical Mode
* Connect switches and end devices using the appropriate cables
* Configure IPv4 addresses on end devices
* Access Cisco switches through a console connection
* Configure basic switch settings using the Cisco IOS CLI
* Configure switch management interfaces
* Configure console and privileged EXEC passwords
* Configure an MOTD banner
* Save switch configurations to NVRAM
* Verify interface status and connectivity using IOS commands and `ping`

---

## Lab Environment

### Network Devices

* Cisco Switch — S1
* Cisco Switch — S2

### End Devices

* PC-A
* PC-B

### Network Topology

```text
PC-A ──── S1 ───── S2 ──── PC-B
         F0/6   F0/1   F0/1   F0/18
```

---

## Addressing

| Device | Interface | IP Address     | Subnet Mask     |
| ------ | --------- | -------------- | --------------- |
| S1     | VLAN 1    | `192.168.1.1`  | `255.255.255.0` |
| S2     | VLAN 1    | `192.168.1.2`  | `255.255.255.0` |
| PC-A   | NIC       | `192.168.1.10` | `255.255.255.0` |
| PC-B   | NIC       | `192.168.1.11` | `255.255.255.0` |

All devices were configured within the `192.168.1.0/24` IPv4 subnet.

---

# Part 1 — Physical Topology Configuration

The network was constructed in Packet Tracer Physical Mode using two switches and two PCs.

### Physical Connections

| Device | Port             | Connected To | Port            | Cable                   |
| ------ | ---------------- | ------------ | --------------- | ----------------------- |
| S1     | FastEthernet0/1  | S2           | FastEthernet0/1 | Copper Cross-Over       |
| S1     | FastEthernet0/6  | PC-A         | FastEthernet0   | Copper Straight-Through |
| S2     | FastEthernet0/18 | PC-B         | FastEthernet0   | Copper Straight-Through |

The PCs were powered on and the physical connections were inspected to verify that the correct ports and cables were being used.

Initially, switch port LEDs may appear amber while the interfaces transition to an operational state. After the network converges, active connections should display green status indicators.

---

# Part 2 — PC Configuration

Static IPv4 addressing was configured on both PCs through:

**Desktop → IP Configuration**

### PC-A

```text
IP Address:  192.168.1.10
Subnet Mask: 255.255.255.0
```

### PC-B

```text
IP Address:  192.168.1.11
Subnet Mask: 255.255.255.0
```

The configuration on PC-A was verified using:

```text
C:\> ipconfig /all
```

Connectivity between the two end devices was then tested:

```text
C:\> ping 192.168.1.11
```

The ping was successful with 0% packet loss.

---

# Part 3 — Basic Switch Configuration

The switches were accessed through a console connection using the end devices.

---

## Hostname

Each switch was configured with its corresponding hostname:

```text
Switch(config)# hostname S1
```

and:

```text
Switch(config)# hostname S2
```

---

## Console Security

Console access was protected using the password specified by the activity:

```text
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
```

The same configuration was applied to S2.

The `login` command enables password authentication on the console line.

---

## Privileged EXEC Security

Privileged EXEC mode was protected using the required password:

```text
S1(config)# enable password class
```

The same configuration was applied to S2.

The `enable password` command protects access to privileged EXEC mode.

> This activity specifically required `class` as the privileged EXEC password and `cisco` for console access.

---

## Management Interface

The switches were configured with IPv4 addresses on the VLAN 1 SVI.

### S1

```text
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.1 255.255.255.0
S1(config-if)# no shutdown
```

### S2

```text
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.1.2 255.255.255.0
S2(config-if)# no shutdown
```

The VLAN 1 SVI provides an IP-based management interface for each switch.

The `no shutdown` command administratively enables the SVI.

---

## MOTD Banner

A Message of the Day banner was configured to warn against unauthorized access:

```text
S1(config)# banner motd "Authorized Access Only!"
```

The same configuration was applied to S2.

The MOTD banner is displayed when a user connects to the device and is commonly used to provide security and access warnings.

---

# Configuration Verification

Several Cisco IOS `show` commands were used to verify the configuration.

### Running Configuration

```text
S1# show running-config
```

This was used to inspect the current configuration, including:

* Hostname
* Console password
* Privileged EXEC password
* VLAN 1 configuration
* MOTD banner

### IOS Version

```text
S1# show version
```

This command displays the IOS version and other system information.

### Interface Status

```text
S1# show ip interface brief
```

This command was used to verify the IP address and operational status of the switch interfaces.

---

# Interface Status

The activity required recording the status of the relevant interfaces after configuration.

| Interface | S1 Status | S1 Protocol | S2 Status | S2 Protocol |
| --------- | --------- | ----------- | --------- | ----------- |
| F0/1      | `up`      | `up`        | `up`      | `up`        |
| F0/6      | `up`      | `up`        | `down`    | `down`      |
| F0/18     | `down`    | `down`      | `up`      | `up`        |
| VLAN 1    | `up`      | `up`        | `up`      | `up`        |

The interface states reflect the physical connections present on each switch.

* **F0/1** connects S1 to S2.
* **F0/6** connects S1 to PC-A.
* **F0/18** connects S2 to PC-B.
* **VLAN 1** provides the management SVI.

> Interface status may vary temporarily while Packet Tracer initializes the topology.

---

# Saving the Configuration

The switch configurations were saved to NVRAM using:

```text
S1# copy running-config startup-config
S2# copy running-config startup-config
```

This ensures that the configuration is preserved after a device restart.

---

# Connectivity Verification

Connectivity was verified using `ping`.

### PC-A → PC-B

```text
PC-A> ping 192.168.1.11
```

### PC-A → S1

```text
PC-A> ping 192.168.1.1
```

### PC-A → S2

```text
PC-A> ping 192.168.1.2
```

The switches were also used to test connectivity with the PCs.

Successful ping responses confirmed that the devices were correctly addressed and connected within the same IPv4 subnet.

---

# Reflection

## Why are some FastEthernet ports active while others are inactive?

A switch port becomes active when it has a connected and operational device or link.

In this topology:

* S1 F0/1 is active because it connects to S2.
* S1 F0/6 is active because it connects to PC-A.
* S2 F0/1 is active because it connects to S1.
* S2 F0/18 is active because it connects to PC-B.
* Other unused switch ports remain inactive because they have no active physical connection.

---

## What can prevent a ping from being sent between the PCs?

Several problems can prevent connectivity, including:

* Incorrect IP address
* Incorrect subnet mask
* Incorrect cable type or port connection
* Interface being administratively down
* Interface or physical link being down
* Incorrect switch configuration
* Devices being placed in different IP subnets

In this lab, both PCs were configured in the same `192.168.1.0/24` subnet, allowing direct Layer 2 communication.

---

# Key Commands

| Purpose                       | Command                              |
| ----------------------------- | ------------------------------------ |
| Enter Privileged EXEC         | `enable`                             |
| Enter Global Configuration    | `configure terminal`                 |
| Configure hostname            | `hostname S1`                        |
| Configure console             | `line console 0`                     |
| Configure console password    | `password cisco`                     |
| Enable console authentication | `login`                              |
| Configure privileged password | `enable password class`              |
| Configure MOTD                | `banner motd "message"`              |
| Enter management SVI          | `interface vlan 1`                   |
| Configure IP address          | `ip address <ip> <mask>`             |
| Enable SVI                    | `no shutdown`                        |
| Verify running configuration  | `show running-config`                |
| Verify IOS version            | `show version`                       |
| Verify interface status       | `show ip interface brief`            |
| Save configuration            | `copy running-config startup-config` |
| Test connectivity             | `ping <ip>`                          |

---

# Key Takeaways

This lab reinforced several fundamental networking concepts:

* Physical Ethernet topology and cable selection
* Console-based Cisco IOS access
* Cisco IOS configuration modes
* Hostname configuration
* Console and privileged EXEC authentication
* Switch management through an SVI
* IPv4 addressing and subnet masks
* Interface operational states
* Configuration persistence through NVRAM
* Basic Layer 2 connectivity
* Network troubleshooting using `show` commands and `ping`

The lab also demonstrated an important distinction between a switch's **physical interfaces** and its **SVI**. Physical interfaces provide connectivity to network devices, while the VLAN 1 SVI provides an IP interface that can be used to manage the switch.

---

## Result

The physical LAN was successfully assembled and configured using:

```text
PC-A       192.168.1.10
S1 VLAN 1  192.168.1.1
S2 VLAN 1  192.168.1.2
PC-B       192.168.1.11
```

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/9f2edb84-b07d-4cba-be15-a7920fc750da" />

Connectivity between the PCs and switches was verified using `ping`, and the switch configurations were saved to NVRAM.
