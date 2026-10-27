# Lab 02 — IOS Console Connectivity (Physical Mode)

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/488145cb-0753-423f-a10f-b25cecb1a295" />

# Lab 02 — IOS Console Connectivity (Physical Mode)

## Overview

This Packet Tracer Physical Mode activity explored local console access to Cisco devices using both serial console and Mini-USB connections.

The lab focused on physically installing Cisco devices, establishing console sessions, accessing Cisco IOS, verifying device information, and configuring the system clock.

## Objectives

* Access a Cisco Catalyst 2960 switch through the serial console port
* Establish a console session using Packet Tracer Terminal
* Verify the switch IOS version
* Configure and verify the system clock
* Access a Cisco ISR 4321 router through the Mini-USB console port
* Explore the physical interfaces of Cisco networking devices

---

## Lab Environment

### Network Devices

* Cisco Catalyst 2960 Switch
* Cisco ISR 4321 Router

### End Devices

* PC
* Laptop

### Console Connections

```text
PC (RS-232)
     │
     │ Console Rollover Cable
     ▼
Catalyst 2960 Console Port
```

```text
Laptop (USB)
     │
     │ Mini-USB Console Cable
     ▼
ISR 4321 Mini-USB Console Port
```

---

## Part 1 — Serial Console Access and Switch Configuration

### Physical Device Inspection

The Cisco Catalyst 2960 switch was installed in the rack and inspected in Physical Mode.

The following interfaces were identified:

* 24 Fast Ethernet ports for end-device connections
* 2 additional ports for network-device connections
* Console port for local CLI access

The PC was also inspected to identify its:

* Fast Ethernet interface
* RS-232 serial interface
* USB interfaces

### Console Connection

A rollover console cable was used to connect:

```text
PC RS-232 → Catalyst 2960 Console
```

### Terminal Configuration

The Packet Tracer Terminal was configured using the default console parameters:

```text
Baud Rate:    9600
Data Bits:    8
Parity:       None
Stop Bits:    1
Flow Control: None
```

After opening the terminal and pressing `ENTER`, the switch presented the User EXEC prompt:

```text
Switch>
```

---

### IOS Verification

The IOS version was verified using:

```text
Switch> show version
```

The switch was running:

```text
Cisco IOS Software, C2960 Software
Version 12.2(25)FX
```

---

### Clock Configuration

The initial system clock was checked with:

```text
Switch> show clock
```

Output:

```text
*00:30:05.261 UTC Mon Mar 1 1993
```

The `enable` command was used to enter Privileged EXEC mode:

```text
Switch> enable
Switch#
```

Context-sensitive help was then used to determine the required syntax:

```text
Switch# clock set ?

hh:mm:ss  Current Time
```

The next parameter was identified with:

```text
Switch# clock set 16:47:00 ?

<1-31>  Day of the month
MONTH   Month of the year
```

The clock was configured as required by the lab:

```text
Switch# clock set 16:47:00 Sep 28 2026
```

### Verification

The configuration was verified using:

```text
Switch# show clock
```

Output:

```text
16:47:55.593 UTC Mon Sep 28 2026
```

✅ **Clock successfully configured.**

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/24e7e4b0-17ac-49c7-83d1-39c17248aff5" />

---

## Part 2 — Mini-USB Console Access to the Router

### Router Installation

A Cisco ISR 4321 router was installed in the rack and inspected in Physical Mode.

The following interfaces were identified:

* RJ-45 interfaces
* Mini-USB console interface
* Power switch

### Laptop Inspection

The laptop was inspected to identify its available interfaces, including:

* RS-232
* Fast Ethernet
* USB ports

### Mini-USB Console Connection

A Mini-USB console cable was used to connect:

```text
Laptop USB → ISR 4321 Mini-USB Console
```

### Router Console Session

The Packet Tracer Terminal was opened on the laptop.

After the router completed its startup process, the initial configuration dialog appeared:

```text
Would you like to enter the initial configuration dialog? [yes/no]:
```

The response was:

```text
n
```

After pressing `ENTER`, the router entered User EXEC mode:

```text
Router>
```

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/8f4328e4-d318-4ed2-9371-255a435f37f4" />

---

## Reflection

### 1. How can unauthorized console access be prevented?

Unauthorized console access can be mitigated by:

* Restricting physical access to networking equipment
* Keeping switches and routers in secure rooms or racks
* Configuring console authentication and passwords
* Applying appropriate physical security controls

### 2. Serial Console vs. USB Console

| Connection         | Advantages                                | Disadvantages                                   |
| ------------------ | ----------------------------------------- | ----------------------------------------------- |
| **Serial Console** | Widely supported and reliable             | May require an RS-232 port or adapter           |
| **USB Console**    | Convenient for modern laptops and devices | May require drivers and device-specific support |

---



