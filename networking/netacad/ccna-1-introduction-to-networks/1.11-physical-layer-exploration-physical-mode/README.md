# Lab 02 — Physical Layer Exploration — Physical Mode

<img width="1439" height="899" alt="Physical Layer Exploration — Physical Mode" src="https://github.com/user-attachments/assets/0b0db7d4-d83e-4ee7-9228-1f4c98fb9a39" />

## Overview

This Packet Tracer lab explored how IP packets travel through physical network infrastructure between a client and a remote web server.

Using **Physical Mode**, the activity traced a simulated connection from a home network in Monterey, California, to the University of Hawaii in Honolulu, Hawaii.

The lab combined local IP addressing, `tracert`, ISP infrastructure, autonomous systems, Internet Exchange Points (IXPs), submarine cables, and physical network topology to demonstrate how packets travel across multiple networks before reaching their destination.

---

## Objectives

* Examine local IPv4 addressing information
* Identify private and public IPv4 addresses
* Identify the default gateway
* Examine the physical connection between a home network and an ISP
* Use `tracert` to trace the path between source and destination
* Identify individual hops in a traceroute
* Investigate ISP Points of Presence (PoPs)
* Investigate ISP infrastructure and domain names
* Identify autonomous systems involved in packet forwarding
* Investigate Internet Exchange Points (IXPs)
* Explore Internet2 network infrastructure
* Investigate submarine cable connectivity
* Understand how physical infrastructure supports Internet communication

---

# Part 1 — Examine Local IP Addressing Information

## 1. Local IPv4 Address

The `ipconfig` command was used on the Home PC to examine its local IP addressing information.

```text
C:\> ipconfig
```

The Packet Tracer Home PC uses:

| Parameter       | Value           |
| --------------- | --------------- |
| IPv4 Address    | `192.168.0.75`  |
| Subnet Mask     | `255.255.255.0` |
| Default Gateway | `192.168.0.1`   |

The address `192.168.0.75` is a **private IPv4 address**.

Private IPv4 addresses are used inside local networks and are not directly routable across the public Internet.

---

## 2. Default Gateway

The local router uses the following IPv4 address:

```text
192.168.0.1
```

The default gateway is the router responsible for forwarding traffic from the local network toward external networks.

---

## 3. Public IPv4 Address

The public IPv4 address was obtained by using an Internet IP lookup service.

Unlike the private IPv4 address assigned to the Home PC, the public IPv4 address identifies the network's Internet connection from the perspective of external networks.

The public address, ISP, and geographical information depend on the actual Internet connection being used.

> **Note:** Public IPv4 addresses and ISP geolocation information are dynamic and can change over time. Geolocation databases may also provide an approximate or inaccurate physical location.

---

## 4. Physical Connection to the Internet

The local network consists of the client device, home router, and the ISP's access network.

The connection between the local network and the ISP can use different technologies, including:

* Cable
* DSL
* Fiber-optic
* Cellular
* Satellite
* Wireless local loop

The exact technology depends on the Internet service used at the location.

---

# Part 2 — Trace the Path Between Source and Destination

## 1. Using `tracert`

The path to the University of Hawaii web server was investigated using:

```text
C:\> tracert www.hawaii.edu
```

The Packet Tracer simulation follows a connection from Monterey, California, to Honolulu, Hawaii.

An example traceroute from the activity was:

```text
1   3 ms   4 ms   3 ms   10.0.0.1
2  13 ms  16 ms  11 ms   10.120.89.61
3  44 ms  18 ms  18 ms   po-302-1222-rur02.monterey.ca.sfba.comcast.net
4  13 ms  14 ms  13 ms   po-2-rur01.monterey.ca.sfba.comcast.net
5  21 ms  17 ms  15 ms   be-222-rar01.santaclara.ca.sfba.comcast.net
6  16 ms  20 ms  19 ms   be-39931-cs03.sunnyvale.ca.ibone.comcast.net
7  27 ms  14 ms  20 ms   be-1312-cr12.sunnyvale.ca.ibone.comcast.net
8  24 ms  19 ms  23 ms   be-303-cr01.9greatoaks.ca.ibone.comcast.net
9  19 ms  21 ms  17 ms   be-2211-pe11.9greatoaks.ca.ibone.comcast.net
10 16 ms  23 ms  16 ms   ae-3.2011.rtsw.sunn.net.internet2.edu
11 24 ms  24 ms  23 ms   et-2-3-0.3457.rtsw.losa.net.internet2.edu
12 85 ms  87 ms  85 ms   172.16.47.134
13 87 ms  85 ms  85 ms   xe-1-1-0-54-kolanut-re0.uhnet.net
14 87 ms  86 ms  87 ms   vl-669-10gigcolol3.uhnet.net
15  *      *      *       Request timed out.
16  *      *      *       Request timed out.
```

The traceroute demonstrates that the packet does not travel directly from the client to the destination. Instead, it passes through multiple routers, or **hops**.

---

## 2. Understanding Hops

Each hop represents a router that forwarded the packet toward its destination.

For example:

```text
1   3 ms  4 ms  3 ms  10.0.0.1
```

The three time values represent the round-trip time measured for the probes sent to that hop.

The final value identifies the router interface that responded to the traceroute request.

Some routers also provide a domain name that can reveal information about their network or approximate location.

---

# 3. The ISP Point of Presence

The second hop represents the first router outside the local home network.

This router belongs to the ISP and is known as a **Point of Presence (POP)**.

The connection between the customer's premises and the ISP's POP is commonly referred to as the:

* Local loop
* Last mile

The local loop can use technologies such as:

* Cable
* DSL
* Fiber
* Cellular
* Satellite
* Wireless

---

# 4. Comcast POP

In the Packet Tracer simulation, the Home Router is connected to a cable modem.

The cable modem connects to the ISP infrastructure represented by the **Comcast POP**.

The cable modem itself does not appear as a hop in the traceroute because it is not functioning as a Layer 3 router.

Inside the simulated Comcast POP are devices representing ISP infrastructure, including:

* Cable Modem Termination System (CMTS)
* Comcast POP router
* Multilayer switch
* DNS server
* Web server

The DNS server resolves names such as:

```text
www.hawaii.edu
www.tellmemyip.com
```

---

# 5. Comcast Network

The first major section of the path belongs to Comcast.

The example traceroute shows Comcast routers from hops **2 through 9**.

```text
Hop 2  → ISP POP
Hop 3  → Monterey
Hop 4  → Monterey
Hop 5  → Santa Clara
Hop 6  → Sunnyvale
Hop 7  → Sunnyvale
Hop 8  → San Jose / 9 Great Oaks
Hop 9  → San Jose / 9 Great Oaks
```

The router domain names provide clues about the approximate locations:

```text
monterey.ca
santaclara.ca
sunnyvale.ca
9greatoaks.ca
```

The `sfba` portion refers to the **San Francisco Bay Area**.

---

# 6. Why Other Interface Addresses Are Not Shown

A router may have several interfaces, but traceroute only reports the interface that responds to the traceroute packet.

Therefore, the IP addresses assigned to the router's other interfaces are not necessarily displayed.

Traceroute shows the interfaces involved in forwarding the packet along the observed path, rather than providing a complete inventory of every interface on every router.

---

# 7. Domain Names as Location Clues

Router hostnames can sometimes provide useful information about network topology and approximate physical location.

Examples from the activity include:

```text
po-302-1222-rur02.monterey.ca.sfba.comcast.net
po-2-rur01.monterey.ca.sfba.comcast.net
be-222-rar01.santaclara.ca.sfba.comcast.net
be-39931-cs03.sunnyvale.ca.ibone.comcast.net
be-1312-cr12.sunnyvale.ca.ibone.comcast.net
be-303-cr01.9greatoaks.ca.ibone.comcast.net
be-2211-pe11.9greatoaks.ca.ibone.comcast.net
```

These names can reveal:

* ISP ownership
* Approximate location
* Router role
* Network hierarchy

However, domain naming conventions are controlled by network administrators and are not guaranteed to represent the exact physical location.

---

# 8. Internet Exchange Point

At approximately hop 9, the traffic reaches the edge of the Comcast network.

The hostname contains:

```text
9greatoaks.ca
```

The activity identifies this location as **Equinix SV5**, an Internet Exchange Point (IXP) in San Jose, California.

An IXP provides infrastructure where different networks can exchange traffic.

In this example, Comcast exchanges traffic with **Internet2**.

---

# 9. Internet2

The next section of the route belongs to Internet2.

The traceroute identifies:

```text
Hop 10 → Internet2
Hop 11 → Internet2
Hop 12 → Internet2
```

Internet2 is a nonprofit networking organization serving research, education, government, and related communities.

The activity demonstrates how traffic can move from a commercial ISP to another autonomous system through an Internet exchange point.

---

# 10. Link to Los Angeles

Hop 11 contains:

```text
et-2-3-0.3457.rtsw.losa.net.internet2.edu
```

The `losa` portion provides a clue that the router is located in the **Los Angeles** area.

At this point, packets have traveled south from the San Francisco Bay Area toward Los Angeles before crossing the Pacific Ocean.

---

# 11. Submarine Cable Across the Pacific

A significant increase in round-trip time occurs between hops 11 and 12.

Example:

```text
Hop 11 → ~24 ms
Hop 12 → ~85 ms
```

This large increase indicates that the packet has traveled a much greater physical distance.

The activity uses this difference to infer that the traffic has crossed the Pacific Ocean between California and Hawaii.

The simulated physical path crosses a submarine cable between the continental United States and Hawaii.

---

## SEA-US Cable

The activity identifies the **SEA-US** submarine cable as the cable connecting the continental United States with Hawaii.

The cable provides connectivity between Hawaii and the mainland United States and forms part of the physical infrastructure carrying Internet traffic across the Pacific.

---

# 12. Submarine Cable Repeaters

Submarine cables contain optical repeaters along their route.

These repeaters regenerate or amplify optical signals so that communication can travel across very long distances.

The Packet Tracer simulation only displays a small number of repeaters even though a real submarine cable contains many more.

---

# 13. Hawaii and Internet2 Peer Exchange

After crossing the Pacific, the packet reaches the Internet2 infrastructure in Hawaii.

Hop 12 represents the final Internet2 router before the traffic is handed over to the University of Hawaii network.

The activity identifies this infrastructure as the **Internet2 Peer Exchange (IP2X)** in Hawaii.

---

# 14. University of Hawaii Network

The next hop belongs to the University of Hawaii network:

```text
13  ... xe-1-1-0-54-kolanut-re0.uhnet.net
```

The domain:

```text
uhnet.net
```

indicates that the router belongs to the University of Hawaii network.

The route then continues through additional University of Hawaii infrastructure.

---

# 15. Traceroute Timeouts

Eventually, the traceroute begins to return:

```text
* * * Request timed out.
```

A timeout does not necessarily mean that the destination is unreachable.

Routers, firewalls, or servers may be configured not to respond to traceroute messages.

In the example, the traceroute stops receiving responses after hop 14.

Despite the timeout, the previous hops provide enough information to trace the physical path from California to Hawaii.

---

# Autonomous Systems

The activity demonstrates three major autonomous systems:

| Autonomous System    | Role                           |
| -------------------- | ------------------------------ |
| Comcast              | Commercial ISP                 |
| Internet2            | Research and education network |
| University of Hawaii | Educational network            |

An **Autonomous System (AS)** is a network or collection of networks operated under a common routing policy.

The Internet is composed of thousands of interconnected autonomous systems.

Traffic is forwarded between these systems through interconnection points and routing relationships.

---

# Packet Path Summary

The simulated packet path can be summarized as:

```text
Home PC
   ↓
Home Router
   ↓
Cable Modem
   ↓
Comcast POP
   ↓
Comcast Network
   ↓
San Jose / Equinix IXP
   ↓
Internet2
   ↓
Los Angeles
   ↓
Submarine Cable
   ↓
Hawaii / IP2X
   ↓
University of Hawaii Network
   ↓
University of Hawaii Web Server
```

This demonstrates that Internet communication depends on a combination of:

* End devices
* Local routers
* ISP infrastructure
* Data centers
* Internet Exchange Points
* Autonomous systems
* Long-distance fiber networks
* Submarine cables
* Routers at the destination network

---

# Key Concepts

## Private vs. Public IPv4

Private IPv4 addresses are used inside local networks.

Public IPv4 addresses are globally routable and are used for communication across the Internet.

## Default Gateway

The default gateway is the router used by a host to reach networks outside its local subnet.

## Traceroute

`tracert` identifies the routers encountered along a path to a destination.

```text
tracert www.hawaii.edu
```

Each router along the path represents a hop.

## ISP Point of Presence

A POP is a physical location where an ISP provides network access to its customers.

## Local Loop

The local loop, or last mile, is the connection between the customer's network and the ISP's access infrastructure.

## Internet Exchange Point

An IXP provides infrastructure where independent networks can exchange traffic.

## Autonomous System

An AS is a network or collection of networks operated under a common routing policy.

## Submarine Cable

Submarine fiber-optic cables provide high-capacity communication links between geographically distant regions across oceans.

## Round-Trip Time

Traceroute reports the time required for packets to travel to a hop and for the corresponding response to return.

A significant increase in RTT can provide clues about a major increase in physical distance.

---

# Result

✅ Examined local IPv4 addressing

✅ Identified the default gateway

✅ Distinguished private and public IPv4 addressing

✅ Investigated local network connectivity

✅ Used `tracert` to analyze a network path

✅ Identified individual hops

✅ Investigated ISP POP infrastructure

✅ Analyzed router domain names

✅ Investigated Comcast network infrastructure

✅ Identified an Internet Exchange Point

✅ Investigated Internet2

✅ Traced the path toward Los Angeles

✅ Investigated the Pacific submarine cable connection

✅ Investigated the Hawaii Internet2 infrastructure

✅ Investigated the University of Hawaii network

✅ Learned why traceroute requests can time out

✅ Connected the physical infrastructure to the logical path of IP packets

---

## Conclusion

This lab demonstrated that an Internet connection is not a single direct link between a client and a server.

Instead, packets travel through multiple networks, routers, data centers, exchange points, and long-distance physical links.

The traceroute provided a logical representation of the path, while **Physical Mode** allowed the corresponding physical infrastructure to be explored.

The most important takeaway is that the Internet is an **interconnection of autonomous systems and physical networks**. A packet traveling from one location to another may cross multiple organizations and technologies before reaching its destination.
