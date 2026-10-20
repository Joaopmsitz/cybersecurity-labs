# Day 8 — Configuring IP Addresses

![Initial Packet Tracer topology](./images/1ccna.png)

Lab completed as part of **Jeremy's IT Lab — Free CCNA 200-301 Complete Course**.

## Topics

- IPv4 addressing
- Subnet masks and CIDR notation
- Router interface configuration
- Cisco IOS CLI
- Interface activation with `no shutdown`
- Default gateway configuration
- ICMP connectivity testing with `ping`
- Configuration verification and saving

## Lab

Configured IPv4 addressing on router R1 and three PCs connected to separate IP networks using Cisco Packet Tracer.

The lab involved assigning IP addresses and subnet masks to R1's GigabitEthernet interfaces, enabling the interfaces, configuring the PCs' network settings, and testing connectivity between PC1, PC2, and PC3.

## Addressing Plan

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| R1 | G0/0 | 15.255.255.254 | 255.0.0.0 | N/A |
| R1 | G0/1 | 182.98.255.254 | 255.255.0.0 | N/A |
| R1 | G0/2 | 201.191.20.254 | 255.255.255.0 | N/A |
| PC1 | NIC | 15.0.0.1 | 255.0.0.0 | 15.255.255.254 |
| PC2 | NIC | 182.98.0.1 | 255.255.0.0 | 182.98.255.254 |
| PC3 | NIC | 201.191.20.1 | 255.255.255.0 | 201.191.20.254 |

## Configuration

Configured the router hostname, assigned IPv4 addresses to the three GigabitEthernet interfaces, and enabled each interface.

```cisco
enable
configure terminal
hostname R1

interface g0/0
 ip address 15.255.255.254 255.0.0.0
 no shutdown
 exit

interface g0/1
 ip address 182.98.255.254 255.255.0.0
 no shutdown
 exit

interface g0/2
 ip address 201.191.20.254 255.255.255.0
 no shutdown
 exit

end
```

The IP addresses, subnet masks, and default gateways for PC1, PC2, and PC3 were configured through the PC configuration interfaces in Packet Tracer.

## Verification

Verified the router interface IP addresses and operational status using:

```cisco
show ip interface brief
```

Reviewed the active router configuration using:

```cisco
show running-config
```

Saved the configuration to NVRAM:

```cisco
copy running-config startup-config
```

## R1 Interface Configuration

![R1 configuration](./images/2ccna.png)

## Connectivity Tests

Tested connectivity from PC1 to PC2 and PC3 using ICMP echo requests.

```text
ping 182.98.0.1
ping 201.191.20.1
```

The ping tests were used to verify end-to-end connectivity between the PCs on the three networks.

![Ping tests to PC2 and PC3](./images/3ccna.png)

## Tool

- Cisco Packet Tracer

## Reference

Jeremy's IT Lab — Free CCNA 200-301 Complete Course

Day 8 — IPv4 Addresses
