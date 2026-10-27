# Day 6 — MAC Address Table

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/cb138ff9-18ed-4c8c-9600-4d28e114e4b5" />

Lab completed as part of **Jeremy's IT Lab — Free CCNA 200-301 Complete Course**.

## Topics

* MAC address tables
* MAC address learning
* ARP
* Broadcast and unicast traffic
* Ethernet frame forwarding
* MAC address table verification
* Clearing dynamic MAC addresses
* Cisco IOS CLI
* Cisco Packet Tracer Simulation Mode

## Lab

Investigated how switches learn MAC addresses and how ARP and ICMP traffic are forwarded across the network.

The lab started with empty MAC address tables on both switches and empty ARP tables on all PCs.

Before the first ping, PC1 did not know the MAC address associated with PC3's IP address, so it generated an ARP Request. The broadcast was flooded by the switch to the other devices in the same broadcast domain.

After receiving the ARP Reply from PC3, PC1 learned its MAC address and was able to send the ICMP Echo Request directly to PC3.

Additional ping traffic was then generated to allow the switches to learn the MAC addresses of the PCs.

## Verification

Used Packet Tracer's **Simulation Mode** to observe ARP and ICMP traffic.

The following commands were used to inspect the switch MAC address tables:

```text
show mac address-table
show mac address-table dynamic
```

Dynamic MAC address entries were then cleared with:

```text
clear mac address-table dynamic
```

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/87560d90-ff64-4c2f-9258-dcf53011ddf2" />


## Tool

* Cisco Packet Tracer

## Reference

Jeremy's IT Lab — Free CCNA 200-301 Complete Course
Day 6 — MAC Address Table
