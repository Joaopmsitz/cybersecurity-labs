
# Activity 11.09 — Using OpenVPN on Kali Linux

## Objective

Configure and establish a VPN connection using OpenVPN on Kali Linux, verify the change in the public IP address during the connection, and compare the address displayed before and after disconnection.

## Environment

- **Operating system:** Kali GNU/Linux
- **Tool:** OpenVPN
- **Service used in the lab:** VPNBook
- **Configuration file:** `vpnbook-ca149-tcp80.ovpn`
- **VPN server used:** CA149
- **Protocol:** TCP
- **Port:** 80

> **Note:** The credentials used to authenticate with VPNBook are not recorded in this document.

## 1. Obtaining the Configuration File

The VPNBook website was accessed:

https://www.vpnbook.com/

On the service page, a free OpenVPN server located outside the United States was selected.

The following server was used for this activity:

```text
CA149
```

The OpenVPN configuration package was downloaded.

The compressed file was extracted into the following directory:

```text
/home/aluno/Downloads/
```

After extraction, the following directory was created:

```text
/home/aluno/Downloads/vpnbook-openvpn-ca149/
```

This directory contained the files required to establish a connection to the VPN server.

## 2. Obtaining Administrative Access

The Kali Linux Terminal was opened, and administrative privileges were obtained using:

```bash
sudo -i
```

## 3. Accessing the Configuration Files

The directory containing the extracted files was accessed:

```bash
cd /home/aluno/Downloads/vpnbook-openvpn-ca149/
```

The configuration file used in the activity was:

```text
vpnbook-ca149-tcp80.ovpn
```

## 4. Starting the OpenVPN Connection

The connection was started using:

```bash
openvpn --config vpnbook-ca149-tcp80.ovpn
```

During initialization, OpenVPN displayed several warnings related to the configuration used by the file.

The initial output was:

```text
2025-12-05 23:19:51 DEPRECATED: --persist-key option ignored. Keys are now always persisted across restarts.
2025-12-05 23:19:51 WARNING: Compression for receiving enabled. Compression has been used in the past to break encryption. Compression support is deprecated and we recommend to disable it completely.
2025-12-05 23:19:51 DEPRECATED OPTION: --cipher set to 'AES-256-CBC' but missing in --data-ciphers (DEFAULT). OpenVPN ignores --cipher for cipher negotiations.
2025-12-05 23:19:51 Note: '--allow-compression' is not set to 'no', disabling data channel offload.
2025-12-05 23:19:51 OpenVPN 2.7_rc2 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] [DCO]
2025-12-05 23:19:51 library versions: OpenSSL 3.5.4 30 Sep 2025, LZO 2.10
2025-12-05 23:19:51 DCO version: N/A
Enter Auth Username: vpnbook
Enter Auth Password: •••••••
```

Authentication was performed using the credentials provided by VPNBook.

The following output displayed an important warning about server certificate verification:

```text
2025-12-05 23:20:12 WARNING: No server certificate verification method has been enabled.  See http://openvpn.net/howto.html#mitm for more info.
```

This warning indicates that the configuration used in the lab did not have a server certificate verification method enabled.

OpenVPN then established the connection to the remote server:

```text
2025-12-05 23:20:12 TCP/UDP: Preserving recently used remote address: [AF_INET]144.217.253.149:80
2025-12-05 23:20:12 Socket Buffers: R=[131072->131072] S=[16384->16384]
```

After negotiation, DNS and the data channel were configured:

```text
2025-12-05 23:20:13 /usr/libexec/openvpn/dns-updown
setting DNS using resolv.conf file
2025-12-05 23:20:13 dns up command exited with status 0
2025-12-05 23:20:13 Data Channel: cipher 'AES-256-GCM', peer-id: 11, compression: 'lzo'
2025-12-05 23:20:13 Timers: ping 5, ping-restart 30
2025-12-05 23:20:13 Protocol options: protocol-flags cc-exit tls-ekm dyn-tls-crypt
```

Routes were also added to direct traffic through the VPN:

```text
2025-12-05 23:20:15 net_route_v4_add: 144.217.253.149/32 via 192.168.98.1 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 0.0.0.0/1 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 128.0.0.0/1 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 10.12.0.1/32 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 Initialization Sequence Completed
```

The message:

```text
Initialization Sequence Completed
```

indicates that the OpenVPN initialization sequence was completed and the VPN connection was established.

## 5. Verifying the Public IP Address

With the VPN active, a browser was opened and the following website was accessed:

https://whatismyipaddress.com/

The public IP address displayed during the VPN connection was:

```text
My IP Address is:
IPv4: ? 144.217.253.149
IPv6: ? Not detected

My IP Information:

ISP: OVH Hosting Inc.
Services: Network Sharing Device
City: Trois-Rivières
Region: Quebec
Country: Canada
```

The result shows that, during the connection to the VPN server, the lookup service identified the following public IP address:

```text
144.217.253.149
```

and associated the address with OVH infrastructure in Canada.

### Evidence — Step 13

**Caption to include before the screenshot:**

> Screenshot of Activity 11.09: the IP lookup page after the OpenVPN connection was established, showing the public IP address and the location information associated with the VPN exit point.

[**View Evidence — Module 11 / Classes 43–44**](../evidencias.pdf)

## 6. Terminating the VPN Connection

After verifying the IP address, the OpenVPN process was interrupted using:

```text
Ctrl + C
```

This terminated the connection to the VPN server.

## 7. Verifying the IP Address Again

After disconnecting from the VPN, the following page was refreshed:

https://whatismyipaddress.com/

The result displayed in the lab environment was:

```text
My IP Address is:
IPv4: ? 18.234.103.188
IPv6: ? Not detected

My IP Information:

ISP: Amazon Technologies Inc.
City: Ashburn
Region: Virginia
Country: United States
```

At this point, the public IP address displayed was:

```text
18.234.103.188
```

The result differed from the address displayed during the VPN connection.

## 8. Removing the Lab Files

After completing the tests, the Downloads directory was accessed:

```bash
cd /home/aluno/Downloads
```

The existing files were listed:

```bash
ls
```

The result was:

```text
cacert.der vpnbook-openvpn-ca149 vpnbook-openvpn-ca149.zip
```

The files used in the activity were then removed:

```bash
rm -r *
```

The system requested confirmation before proceeding with the removal:

```text
zsh: sure you want to delete all 2 files in /home/aluno/Downloads [yn]? y
```

The confirmation was provided using:

```text
y
```

## Security Observations

During VPN initialization, OpenVPN displayed several warnings that are relevant to the analysis of this activity.

### Compression Enabled

The log displayed:

```text
WARNING: Compression for receiving enabled.
```

OpenVPN itself indicates that compression has a history of issues related to attacks against encrypted channels and recommends disabling it.

### Certificate Verification

The following warning was also displayed:

```text
WARNING: No server certificate verification method has been enabled.
```

This means that the configuration used in the lab did not enable a server certificate verification method.

### Cipher Configured in the File

OpenVPN also reported:

```text
DEPRECATED OPTION: --cipher set to 'AES-256-CBC' but missing in --data-ciphers (DEFAULT).
```

This warning indicates that the `--cipher` option in the file uses a configuration considered obsolete for current negotiation procedures.

Despite these warnings, the log showed that the established data channel used:

```text
AES-256-GCM
```

These warnings are important because they demonstrate that an established VPN connection does not, by itself, mean that the entire configuration follows the most current security recommendations.

## Key Concepts

- **VPN:** Creates a communication tunnel between a client and a VPN server.
- **OpenVPN:** Software used to establish VPN connections.
- **Public IP address:** An address used to identify a device's Internet-facing connection.
- **Routing:** Determines the paths through which packets are sent.
- **DNS:** Name resolution used during the connection.
- **AES-256-GCM:** A cryptographic algorithm/mode used by the data channel observed in the lab.
- **Initialization Sequence Completed:** A message indicating that the OpenVPN connection initialization has been completed.

## Activity Workflow

```text
Download the VPNBook configuration
          ↓
Run OpenVPN
          ↓
Authenticate
          ↓
Establish the VPN tunnel
          ↓
Configure DNS and routes
          ↓
Initialization Sequence Completed
          ↓
Check the public IP address
          ↓
VPN exit IP address
          ↓
Ctrl + C
          ↓
Disconnect from the VPN
          ↓
Check the IP address again
          ↓
Original exit IP address
```

## Result

An OpenVPN connection was established using the VPNBook CA149 server. During the connection, the observed public IP address was `144.217.253.149`, associated with the VPN exit point in Canada. After disconnection, the environment displayed the public IP address `18.234.103.188` again.

The activity also provided an opportunity to observe security warnings in the configuration used by the lab, including enabled compression, the absence of a server certificate verification method, and the use of an obsolete `--cipher` option.

---

[Back to Classes 43–44](../README.md) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
