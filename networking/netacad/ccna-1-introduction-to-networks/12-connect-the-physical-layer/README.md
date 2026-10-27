# Lab 03 — Connect the Physical Layer

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/1d49017e-366e-4d5c-9c1e-e430af4214f4" />

## Overview

This Packet Tracer lab focused on identifying the physical characteristics of Cisco networking devices, selecting appropriate hardware modules, connecting devices using different physical media, and verifying connectivity.

The activity provided practical experience with router management ports, LAN and WAN interfaces, interface bandwidth, expansion modules, Ethernet and fiber connections, serial WAN connections, and wireless and cellular connectivity.

---

## Objectives

* Identify management, LAN, and WAN interfaces on Cisco devices
* Determine the default bandwidth of different interfaces
* Identify available expansion slots
* Select appropriate modules for additional connectivity
* Install modules in Cisco networking devices
* Connect devices using the appropriate physical media
* Verify interface status using Cisco IOS commands
* Verify wireless and cellular connectivity
* Understand the physical characteristics of network connections

---

## Lab Environment

### Devices

* East Router
* West Router
* Switch1
* Switch2
* Switch3
* Switch4
* Access Point
* PC1–PC9
* Laptop
* TabletPC

### Technologies

* Ethernet
* Fast Ethernet
* Gigabit Ethernet
* Fiber-optic Ethernet
* Serial WAN
* Wireless LAN (WLAN)
* 3G/4G cellular connectivity

---

# Part 1 — Identify Physical Characteristics of Internetworking Devices

## 1. Management Ports

The East router was inspected in the Physical workspace to identify its available management interfaces.

### Available Management Ports

**Answer:** `AUX and Console`

Management ports are used for device administration rather than normal data forwarding.

---

## 2. LAN and WAN Interfaces

The physical interfaces available on the East router were identified.

### LAN Interfaces

**Answer:** `2 GigabitEthernet interfaces**

* GigabitEthernet0/0
* GigabitEthernet0/1

### WAN Interfaces

**Answer:** `2 Serial interfaces`

* Serial0/0/0
* Serial0/0/1

### Physical Interfaces

The following command was used to verify the interfaces:

```bash
East> show ip interface brief
```

The `Vlan1` interface is a virtual interface and therefore does not represent a physical port.

**Number of physical interfaces:** `4`

---

## 3. Interface Bandwidth

The default bandwidth of the GigabitEthernet interface was examined using:

```bash
East> show interface gigabitethernet 0/0
```

**Default bandwidth:** `1,000,000 Kbit/s`

The serial interface was then examined using:

```bash
East> show interface serial 0/0/0
```

**Default bandwidth:** `1,544 Kbit/s`

### Key Concept — Interface Bandwidth

The bandwidth value configured on a Cisco interface is used by routing processes to calculate the best path to a destination.

For serial interfaces, the configured bandwidth value does **not necessarily represent the actual physical bandwidth** of the connection. The actual service speed depends on the WAN service provided by the service provider.

---

## 4. Expansion Slots

The physical workspace was inspected to determine the number of available expansion slots.

| Device      | Available Expansion Slots |
| ----------- | ------------------------: |
| East Router |                         1 |
| Switch2     |                         5 |

Expansion slots allow additional modules to be installed when the device requires additional interfaces or connectivity options.

---

# Part 2 — Select Correct Modules for Connectivity

## 1. Module for Connecting PCs 1–3

The East router needed to provide direct connectivity for PC1, PC2, and PC3 without adding another switch.

### Module Selected

**Answer:** `HWIC-4ESW`

The **HWIC-4ESW** provides four Ethernet switch ports that can be used to connect end devices directly to the router.

### Number of Hosts Supported

**Answer:** `4 hosts`

Although the activity only requires three PCs, the module provides four Ethernet ports.

---

## 2. Module for Gigabit Optical Connectivity

Switch2 needed a Gigabit optical interface to connect to Switch3.

### Module Selected

**Answer:** `PT-SWITCH-NM-1FGE`

This module provides a Gigabit Ethernet fiber-optic interface.

---

## 3. Module Installation

The modules cannot be installed while the devices are powered on because the interfaces are not hot-swappable.

The correct procedure was:

1. Power off the device.
2. Install the required module.
3. Power the device back on.
4. Verify the resulting interface using Cisco IOS.

### Switch2 Module Slot

The following command was used:

```bash
Switch2> show ip interface brief
```

**Module interface:** `GigabitEthernet5/1`

The module was inserted into the expansion slot associated with the `GigabitEthernet5/1` interface.

---

# Part 3 — Connect Devices

The devices were connected using the cable types specified by the activity.

| Device  | Interface          | Cable Type              | Device       | Interface          |
| ------- | ------------------ | ----------------------- | ------------ | ------------------ |
| East    | GigabitEthernet0/0 | Copper Straight-Through | Switch1      | GigabitEthernet0/1 |
| East    | GigabitEthernet0/1 | Copper Straight-Through | Switch4      | GigabitEthernet0/1 |
| East    | FastEthernet0/1/0  | Copper Straight-Through | PC1          | FastEthernet0      |
| East    | FastEthernet0/1/1  | Copper Straight-Through | PC2          | FastEthernet0      |
| East    | FastEthernet0/1/2  | Copper Straight-Through | PC3          | FastEthernet0      |
| Switch1 | FastEthernet0/1    | Copper Straight-Through | PC4          | FastEthernet0      |
| Switch1 | FastEthernet0/2    | Copper Straight-Through | PC5          | FastEthernet0      |
| Switch1 | FastEthernet0/3    | Copper Straight-Through | PC6          | FastEthernet0      |
| Switch4 | GigabitEthernet0/2 | Copper Cross-Over       | Switch3      | GigabitEthernet3/1 |
| Switch3 | GigabitEthernet5/1 | Fiber                   | Switch2      | GigabitEthernet5/1 |
| Switch2 | FastEthernet0/1    | Copper Straight-Through | PC7          | FastEthernet0      |
| Switch2 | FastEthernet1/1    | Copper Straight-Through | PC8          | FastEthernet0      |
| Switch2 | FastEthernet2/1    | Copper Straight-Through | PC9          | FastEthernet0      |
| Switch2 | Gigabit3/1         | Copper Straight-Through | Access Point | Port 0             |
| East    | Serial0/0/0        | Serial DCE              | West         | Serial0/0/0        |

> **Note:** The Serial DCE cable must be connected to the East router first, as specified by the activity.

---

# Part 4 — Check Connectivity

## 1. Verify Interface Status on East

The following command was used:

```bash
East> show ip interface brief
```

The expected output was:

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     172.30.1.1      YES manual up                    up
GigabitEthernet0/1     172.31.1.1      YES manual up                    up
Serial0/0/0            10.10.10.1      YES manual up                    up
Serial0/0/1            unassigned      YES unset  down                  down
FastEthernet0/1/0      unassigned      YES unset  up                    up
FastEthernet0/1/1      unassigned      YES unset  up                    up
FastEthernet0/1/2      unassigned      YES unset  up                    up
FastEthernet0/1/3      unassigned      YES unset  up                    down
Vlan1                  172.29.1.1      YES manual up                    up
```

### Interface Status

The important status combinations are:

| Status | Protocol | Meaning                                                          |
| ------ | -------- | ---------------------------------------------------------------- |
| `up`   | `up`     | Physical and data-link layers are operational                    |
| `down` | `down`   | Physical interface is not operational                            |
| `up`   | `down`   | Physical layer is operational, but the data-link protocol is not |

The interfaces required by the activity were correctly connected.

---

# 2. Verify Wireless Connectivity

The Laptop was configured to use its wireless interface.

### Configuration

1. Open the **Laptop**.
2. Select the **Config** tab.
3. Select **Wireless0**.
4. Enable **Port Status**.
5. Wait for the wireless connection to become active.
6. Open the **Desktop** tab.
7. Open **Web Browser**.
8. Navigate to:

```text
www.cisco.srv
```

The Cisco Packet Tracer webpage was successfully displayed.

---

# 3. Verify TabletPC Wireless Connectivity

The TabletPC was configured in the same way.

### Configuration

1. Open the **TabletPC**.
2. Select the **Config** tab.
3. Select **Wireless0**.
4. Enable **Port Status**.
5. Wait for the wireless connection to become active.
6. Open the **Desktop** tab.
7. Open **Web Browser**.
8. Navigate to:

```text
www.cisco.srv
```

The Cisco Packet Tracer webpage was successfully displayed.

---

# 4. Change the TabletPC Access Method

The TabletPC was then configured to use a cellular connection instead of WLAN.

### Configuration

The **Wireless0** interface was disabled and the **3G/4G Cell1** interface was enabled.

After the cellular connection became active, the web browser was used to access:

```text
www.cisco.pka
```

The Cisco Packet Tracer webpage was successfully displayed.

> **Note:** Wireless0 and 3G/4G Cell1 should not be enabled simultaneously during this activity. Using both interfaces at the same time may cause connectivity problems when accessing network resources.

---

# Key Concepts

## Management Ports

Cisco routers commonly provide dedicated management interfaces such as:

* Console
* AUX

These interfaces provide administrative access to the device.

## LAN and WAN Interfaces

The East router provides:

* **2 GigabitEthernet interfaces** for LAN connectivity
* **2 Serial interfaces** for WAN connectivity

Different interface types are designed for different networking environments.

## Expansion Modules

Expansion modules allow a device to gain additional interfaces or support different physical media.

In this lab:

* `HWIC-4ESW` was used to provide four Ethernet switch ports on the East router.
* `PT-SWITCH-NM-1FGE` was used to provide Gigabit fiber connectivity on Switch2.

## Copper Straight-Through

Traditionally used to connect different types of Ethernet devices, such as:

* Router → Switch
* Switch → PC
* Switch → Access Point

Modern Ethernet devices can support **Auto-MDIX**, which can automatically adjust transmit and receive pairs.

## Copper Cross-Over

Traditionally used to connect similar Ethernet devices, such as:

* Switch → Switch
* Router → Router

In this activity, a copper crossover cable was used between Switch4 and Switch3.

## Fiber-Optic Ethernet

Fiber uses light to transmit data and is commonly used for high-speed network connections and longer distances.

The lab used a fiber connection between:

```text
Switch3 GigabitEthernet5/1
        ↓
Switch2 GigabitEthernet5/1
```

## Serial DCE

The serial connection between East and West uses a **Serial DCE** cable.

The DCE side provides clocking for the serial connection.

In this activity, the DCE cable was connected to the **East router first**, as required by Packet Tracer.

---

# Commands Used

### Display Interface Summary

```bash
show ip interface brief
```

Used to display:

* Interface names
* IP addresses
* Interface status
* Protocol status

### Display GigabitEthernet Information

```bash
show interface gigabitethernet 0/0
```

Used to inspect interface details, including the configured bandwidth.

### Display Serial Interface Information

```bash
show interface serial 0/0/0
```

Used to inspect the serial interface and its configured bandwidth.

---

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/97f06b8e-332f-4139-a723-58fba222c982" />

# Result

✅ Management ports identified

✅ LAN and WAN interfaces identified

✅ Physical interfaces counted

✅ Interface bandwidth values examined

✅ Expansion slots identified

✅ `HWIC-4ESW` module selected and installed

✅ `PT-SWITCH-NM-1FGE` module selected and installed

✅ Devices connected using the appropriate cable types

✅ Serial DCE connection established

✅ Interface status verified using `show ip interface brief`

✅ Laptop wireless connectivity verified

✅ TabletPC wireless connectivity verified

✅ TabletPC cellular connectivity verified

✅ PC connectivity verified

✅ Lab completed successfully
