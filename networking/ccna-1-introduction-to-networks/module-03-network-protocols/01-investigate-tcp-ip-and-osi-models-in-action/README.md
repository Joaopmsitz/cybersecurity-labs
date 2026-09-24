# Lab 01 — Investigate TCP/IP and OSI Models in Action

<img width="1439" height="899" alt="Packet Tracer Simulation Mode" src="https://github.com/user-attachments/assets/bc108905-8e78-4f48-b499-b1f1173d13bd" />

## Overview

This Packet Tracer simulation activity focused on analyzing network communication through the **OSI model** and the **TCP/IP protocol suite**.

Using **Simulation Mode**, HTTP traffic between a Web Client and Web Server was inspected to observe encapsulation, protocol behavior, and communication across different network layers.

---

## Objectives

* Examine HTTP traffic in Simulation Mode
* Analyze the OSI model during network communication
* Observe TCP/IP protocols in action
* Identify PDU information at different layers
* Observe encapsulation and decapsulation
* Examine HTTP, TCP, DNS, ARP, and Ethernet events
* Identify IP addresses, MAC addresses, and port numbers

---

## Lab Environment

### Devices

* Web Client
* Web Server
* Packet Tracer Simulation Mode

### Protocols Observed

* HTTP
* TCP
* DNS
* ARP
* Ethernet

---

# Part 1 — HTTP Traffic

The Web Client accessed:

```text
www.osi.local
```

Packet Tracer was switched to **Simulation Mode**, and HTTP events were analyzed using **Capture/Forward**.

The PDU information was examined through the **OSI Model** and **Outbound PDU Details** tabs.

### OSI Layers Observed

| OSI Layer             | Protocol / Data |
| --------------------- | --------------- |
| Layer 7 — Application | HTTP            |
| Layer 4 — Transport   | TCP             |
| Layer 3 — Network     | IPv4            |
| Layer 2 — Data Link   | Ethernet        |
| Layer 1 — Physical    | Transmission    |

### HTTP Port

```text
TCP/80
```

The Web Server listens for standard HTTP requests on TCP port `80`.

### Encapsulation

```text
HTTP Data
    ↓
TCP Segment
    ↓
IP Packet
    ↓
Ethernet Frame
    ↓
Bits
```

At the destination, the process is reversed through decapsulation.

---

# Part 2 — TCP/IP Protocol Suite

Additional protocol events were enabled in the Simulation Panel.

### DNS

DNS was used to resolve:

```text
www.osi.local
```

into an IP address.

### ARP

ARP was observed resolving an IPv4 address to a MAC address for local network delivery.

### TCP

TCP was observed establishing and terminating the communication session between the client and server.

The general connection process observed was:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

TCP was then used to transport the HTTP communication.

---

# OSI and TCP/IP Relationship

| OSI Model    | TCP/IP Model   | Examples              |
| ------------ | -------------- | --------------------- |
| Application  | Application    | HTTP, DNS             |
| Presentation | Application    | —                     |
| Session      | Application    | —                     |
| Transport    | Transport      | TCP                   |
| Network      | Internet       | IPv4                  |
| Data Link    | Network Access | Ethernet, ARP         |
| Physical     | Network Access | Physical transmission |

---

# Key Findings

The simulation demonstrated the interaction between multiple protocols:

```text
DNS
 ↓
ARP
 ↓
TCP
 ↓
HTTP
```

The activity also demonstrated how data is encapsulated as it moves down the protocol stack and decapsulated when received.

---

# Key Commands / Packet Tracer Functions

| Purpose                 | Function          |
| ----------------------- | ----------------- |
| Enter Simulation Mode   | `Simulation`      |
| Advance network events  | `Capture/Forward` |
| Filter protocols        | `Edit Filters`    |
| Inspect packet          | Click PDU event   |
| Analyze OSI layers      | `OSI Model`       |
| Analyze packet contents | `PDU Details`     |
| Generate Web traffic    | Web Browser       |
| Access Web Server       | `www.osi.local`   |

---

## Result

HTTP communication and the underlying TCP/IP protocols were successfully analyzed using Packet Tracer Simulation Mode.

The activity provided practical visualization of:

* OSI layers
* TCP/IP protocols
* Encapsulation and decapsulation
* DNS resolution
* ARP address resolution
* TCP connection establishment
* HTTP communication
* Transport-layer ports
