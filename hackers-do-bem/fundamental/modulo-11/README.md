# Hackers do Bem — Fundamental | Module 11

This module covers practical networking and security activities involving ARP, network interface configuration, MAC address cloning, Quality of Service (QoS), firewall rules, DNS redirection, VPN connectivity, and ICMP filtering using Kali Linux and Windows Server 2022.

## Activities

### Activities — Class 41–42

| Activity | Topic | Description | View |
|---|---|---|---|
| 11.01 — Exploring the ARP Table on Kali Linux | Cybersecurity Practice | Explore the ARP table on Kali Linux by examining the IP and MAC addresses associated with devices on the network, clearing existing entries, and verifying how new entries are learned again after network communication. | [View](./aula-41-42/atividade-11.01-tabela-arp-kali/README.md) |
| 11.02 — Network Interface Aliases on Kali Linux | Cybersecurity Practice | Configure IP address aliases on the eth0 network interface in Kali Linux by assigning the addresses 192.168.98.41 and 192.168.98.42 to the same physical interface, then validate connectivity using ICMP and SSH. | [View](./aula-41-42/atividade-11.02-alias-interface-rede-kali/README.md) |
| 11.03 — MAC Cloning on Kali Linux | Cybersecurity Practice | Explore how to change the MAC address of a network interface on Kali Linux by temporarily cloning the MAC address of the docker0 interface and then restoring its original MAC address. | [View](./aula-41-42/atividade-11.03-mac-cloning-kali/README.md) |
| 11.04 — QoS on Kali Linux | Cybersecurity Practice | Explore Quality of Service (QoS) mechanisms on Linux using the tc (Traffic Control) command to create queues and filters for controlling traffic on the eth0 interface, and subsequently apply a transmission rate limit. | [View](./aula-41-42/atividade-11.04-qos-kali/README.md) |
| 11.05 — QoS on Windows Server 2022 | Cybersecurity Practice | Configure a Quality of Service (QoS) policy on Windows Server 2022 using the Local Group Policy Editor, set an outbound traffic rate limit, and verify the configuration's impact through a speed test. | [View](./aula-41-42/atividade-11.05-qos-windows-server/README.md) |

### Activities — Class 43–44

| Activity | Topic | Description | View |
|---|---|---|---|
| 11.06 — Exploring ACLs in Windows Server 2022 Firewall | Network Security | Explore the advanced settings of Windows Server 2022 Firewall by examining inbound and outbound rules, connection security rules, and monitoring options related to the firewall and the security associations used in protected communications. | [View](./aula-43-44/atividade-11.06-acl-firewall-windows-server-2022/README.md) |
| 11.07 — Blocking Websites Using iptables on Kali Linux | Cybersecurity Practice | Use iptables on Kali Linux to create a firewall rule that blocks access to the globo.com.br domain, verify the rule, and subsequently remove it to restore access to the website. | [View](./aula-43-44/atividade-11.07-bloqueando-sites-iptables-kali/README.md) |
| 11.08 — Redirecting DNS Requests Using iptables on Kali Linux | Cybersecurity Practice | Use iptables on Kali Linux to redirect DNS requests using a DNAT rule, observe the effect of the change on name resolution, and verify the configuration of the nat table. | [View](./aula-43-44/atividade-11.08-redirecionando-dns-iptables-kali/README.md) |
| 11.09 — Using OpenVPN on Kali Linux | Cybersecurity Practice | Configure and establish a VPN connection using OpenVPN on Kali Linux, verify the change in the public IP address during the connection, and compare the address displayed before and after disconnection. | [View](./aula-43-44/atividade-11.09-openvpn-kali/README.md) |
| 11.10 — Blocking ICMP Packets from Windows Server 2022 on Kali Linux | File Integrity | Use iptables on Kali Linux to block ICMP echo-request packets originating from Windows Server 2022, verify the effect of the rule using the ping command, and subsequently remove the rule to restore communication. | [View](./aula-43-44/atividade-11.10-bloqueando-icmp-windows-server-kali/README.md) |

## Evidence

Evidence files are organized by class. Each PDF consolidates the screenshots and supporting material required for the corresponding practical activities.

- [View Evidence — Class 41–42](./aula-41-42/evidencias.pdf)
- [View Evidence — Class 43–44](./aula-43-44/evidencias.pdf)

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Cybersecurity Portfolio](../../../README.md)
