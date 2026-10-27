# Lab 01 — Connect a Wired and Wireless LAN

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/108182f9-1ddf-49a2-af60-8eb1acb75ca7" />

## Overview

This Packet Tracer lab focused on connecting wired and wireless networks using the appropriate cable types and verifying end-to-end connectivity.

The activity reinforced Physical Layer concepts by requiring the selection of appropriate transmission media, establishing device connections, testing communication, and examining both the physical and logical network topologies.

---

## Objectives

* Connect devices using the appropriate cable types
* Identify straight-through, crossover, serial, coaxial, and console cables
* Verify network connectivity
* Explore logical and physical topologies
* Analyze communication between wired and wireless network segments

---

## Lab Environment

### Devices

* Cloud
* Cable Modem
* Router0
* Router1
* Wireless Router
* Switch
* Configuration Terminal
* NetAcad Server
* Family PC
* Home PC
* Home Printer

### Network Technologies

* Ethernet
* WLAN
* Serial WAN
* Coaxial communication
* TCP/IP

The Wireless Router provided wireless connectivity to:

* Home PC
* Home Printer

---

# Part 1 — Connect to the Cloud

The Cloud was connected to both Router0 and the Cable Modem using different types of physical media.

| From        | To                | Cable Type              |
| ----------- | ----------------- | ----------------------- |
| Cloud Eth6  | Router0 F0/0      | Copper Straight-Through |
| Cloud Coax7 | Cable Modem Port0 | Coaxial                 |

### Key Concept

The Cloud device represents an external network or service-provider infrastructure and can provide different types of connectivity, such as Ethernet and coaxial connections.

---

# Part 2 — Connect Router0

Router0 was connected to several devices using different media types.

| From            | To                           | Cable Type       |
| --------------- | ---------------------------- | ---------------- |
| Router0 S0/0/0  | Router1 S0/0                 | Serial           |
| Router0 F0/1    | NetAcad Server F0            | Copper Crossover |
| Router0 Console | Configuration Terminal RS232 | Console          |

### Key Concepts

#### Serial Cable

A serial connection can be used for WAN communication between routers. In this lab, the serial link connects Router0 and Router1.

#### Copper Crossover

A crossover cable was used for the Ethernet connection between Router0 and the NetAcad Server. Traditionally, crossover cables are used to connect devices with similar Ethernet interfaces.

Modern devices may support **Auto-MDIX**, which can automatically detect and correct transmit/receive pair assignments, reducing the need for crossover cables.

#### Console Cable

A console cable provides out-of-band access to a network device for initial configuration, management, and troubleshooting.

---

# Part 3 — Connect the Remaining Devices

The remaining infrastructure and end devices were connected as follows:

| From                 | To                       | Cable Type              |
| -------------------- | ------------------------ | ----------------------- |
| Router1 F1/0         | Switch F0/1              | Copper Straight-Through |
| Cable Modem Port1    | Wireless Router Internet | Copper Straight-Through |
| Wireless Router Eth1 | Family PC F0             | Copper Straight-Through |

The Wireless Router also provided wireless connectivity to:

* Home PC
* Home Printer

---

# Part 4 — Connectivity Verification

Connectivity was tested from the Family PC using the `ping` command.

### Ping Test

```bash
ping netacad.pka
```

### Result

```text
Pinging 10.0.0.254 with 32 bytes of data:

Reply from 10.0.0.254: bytes=32 time=2ms TTL=126
Reply from 10.0.0.254: bytes=32 time=9ms TTL=126
Reply from 10.0.0.254: bytes=32 time=28ms TTL=126
Reply from 10.0.0.254: bytes=32 time=59ms TTL=126
```

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/f0c85545-1b18-461a-82bf-bc5e5251b8e2" />

### Analysis

The successful ping confirmed end-to-end IP connectivity between the Family PC and the NetAcad Server.

This demonstrates that the devices were correctly interconnected and that communication was successfully established across the network.

---

# Addressing Summary

| Device          | Interface | IP Address     |
| --------------- | --------- | -------------- |
| Router0         | F0/0      | 192.168.2.1/24 |
| Router0         | F0/1      | 10.0.0.1/24    |
| Router0         | S0/0/0    | 172.31.0.1/24  |
| Router1         | S0/0      | 172.31.0.2/24  |
| Router1         | F1/0      | 172.16.0.1/24  |
| Wireless Router | Internet  | 192.168.2.2/24 |
| Wireless Router | Eth1      | 192.168.1.1    |
| Family PC       | F0        | 192.168.1.102  |
| Switch          | F0/1      | 172.16.0.2     |
| NetAcad Server  | F0        | 10.0.0.254     |

---

# Physical Topology Analysis

The Packet Tracer Physical Workspace was explored to examine different networking environments.

### Observations

* Enterprise equipment is commonly installed in racks for organization, management, and scalability.
* Home networks typically use fewer devices and generally do not require dedicated equipment racks.
* Different cable types are used for different networking purposes.
* The physical topology shows how devices and physical media are connected.
* The logical topology focuses on how devices communicate and how the network is structured logically.

---

# Cable Types Used

| Cable Type              | Purpose                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| Copper Straight-Through | Traditionally used to connect different types of Ethernet devices, such as a PC to a switch |
| Copper Crossover        | Traditionally used to connect similar Ethernet devices, such as a router to a server        |
| Serial                  | Used for WAN connections between routers                                                    |
| Coaxial                 | Used for the connection between the Cloud and Cable Modem                                   |
| Console                 | Used for out-of-band device management and configuration                                    |

> **Note:** Modern Ethernet devices may support Auto-MDIX, which allows interfaces to automatically detect and correct the required transmit/receive pair configuration.

---

## Result

✅ Correct cable types selected

✅ Wired devices successfully connected

✅ Wireless devices successfully connected

✅ WAN serial connection established

✅ End-to-end connectivity to the NetAcad Server verified

✅ Console connection established

✅ Physical topology explored

✅ Lab completed successfully
