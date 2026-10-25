# Activity 3.07 — Creating a Honeypot with PentBox on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 11–12  
> **Environment:** Kali Linux and Windows Server 2022  
> **Status:** Completed

## Objective

Configure a honeypot using PentBox on Kali Linux and perform a controlled access test from a Windows Server 2022 machine.

The activity demonstrates how a honeypot can simulate a network-accessible service and record an access attempt, allowing connection details and HTTP request information to be observed.

**Laboratory scope:** All procedures were performed in a controlled environment for academic purposes.

## Environment

- **Operating system:** Kali Linux
- **Tool:** PentBox 1.8
- **Client system:** Windows Server 2022
- **Kali Linux IP address:** `192.168.98.40`
- **Honeypot port:** TCP `80`
- **Client application:** Microsoft Edge

## Procedure

### 1. Obtain Superuser Access

On Kali Linux, the terminal was opened and the following command was executed:

```bash
sudo -i
```

After authentication, the terminal operated as the root user.

### 2. Check the IP Address

The following command was used:

```bash
ifconfig
```

**Observed output:**

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:df:26:13:80  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::1005:27ff:fe44:1631  prefixlen 64  scopeid 0x20<link>
        ether 12:05:27:44:16:31  txqueuelen 1000  (Ethernet)
        RX packets 1818194  bytes 2694820836 (2.5 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61082  bytes 77348531 (73.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Loopback Local)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937  (1.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

The interface used to communicate with the rest of the laboratory environment was `eth0`, configured with the following IP address:

```text
192.168.98.40
```

### 3. Launch PentBox

The PentBox directory was accessed:

```bash
cd /curso/pentbox/pentbox-1.8
```

The program was then launched:

```bash
./pentbox.rb
```

The following main menu was displayed:

```text
PenTBox 1.8 
         __
        U00U|.'@@@@@@`.
        |__|(@@@@@@@@@@)
             (@@@@@@@@)
             `YY~~~~YY'
              ||    ||

--------- Menu          ruby3.1.2 @ x86_64-linux-gnu

1- Cryptography tools

2- Network tools

3- Web

4- Ip grabber

5- Geolocation ip

6- Mass attack

7- License and contact

8- Exit

   ->
```

PentBox provides several tools, including features related to network testing and security.

### 4. Select the Network Tools

The following option was selected from the main menu:

```text
2- Network tools
```

The submenu displayed was:

```text
1- Net DoS Tester
2- TCP port scanner
3- Honeypot
4- Fuzzer
5- DNS and host gathering
6- MAC address geolocation (samy.pl)

0- Back
```

Option `3` was selected to access the honeypot feature.

### 5. Select the Honeypot Feature

The following option was selected:

```text
3- Honeypot
```

PentBox displayed:

```text
// Honeypot //

You must run PenTBox with root privileges.
                                                                                   
 Select option.

1- Fast Auto Configuration
2- Manual Configuration [Advanced Users, more options]
```

The automatic configuration option was selected:

```text
1- Fast Auto Configuration
```

### 6. Activate the Honeypot

After the selection, PentBox reported:

```text
HONEYPOT ACTIVATED ON PORT 80 (2024-01-24 16:52:52 -0500)
```

The honeypot began waiting for connections on TCP port `80`.

Port 80 is conventionally used for HTTP services, allowing a browser access attempt to generate an HTTP request that can be observed by the honeypot.

**Timestamp note:** The activation message contains a timestamp different from the timestamps in the subsequent access-test output. Both outputs are preserved as recorded, but the timestamps should not be assumed to represent the same execution session.

### 7. Test Access from Windows Server 2022

With the honeypot active, the Windows Server 2022 machine provided by the laboratory was accessed.

Microsoft Edge was opened, and the Kali Linux IP address was entered:

```text
http://192.168.98.40
```

The access attempt returned a response indicating that the interaction had been recorded by the honeypot:

```text
Access denied
HTTP Referrer login failed
IP Address login failed
2025-09-06 11:44:50 -0300
```

The date and time shown by the application can vary depending on when the laboratory is run.

### 8. Review the Access Attempt Recorded by the Honeypot

After accessing the Kali Linux address from Windows Server, the Kali Linux terminal was checked again.

PentBox recorded the connection attempt:

```text
INTRUSION ATTEMPT DETECTED! from 192.168.98.30:49736 (2025-09-06 11:45:58 -0300)
-----------------------------
GET / HTTP/1.1
Host: 192.168.98.40
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36 Edg/139.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
```

This record provides several useful details about the HTTP request.

#### Connection Source

```text
from 192.168.98.30:49736
```

This identifies the source IP address and source port observed by the honeypot.

#### HTTP Method

```http
GET / HTTP/1.1
```

Indicates that the browser sent an HTTP `GET` request for the `/` path using HTTP/1.1.

#### Host

```http
Host: 192.168.98.40
```

Identifies the destination host specified in the HTTP request.

#### User-Agent

```http
User-Agent: Mozilla/5.0 (...) Edg/139.0.0.0
```

The `User-Agent` field supplies information about the client making the request. In this case, the recorded string identifies a Chromium-based Microsoft Edge browser running on Windows.

A User-Agent string describes what the client reports; it should not be treated as definitive proof of the browser or operating system identity.

#### Accept

The `Accept` header indicates the content types the client declares it can receive.

#### Accept-Encoding

```http
Accept-Encoding: gzip, deflate
```

Specifies compression methods accepted by the client.

#### Accept-Language

```http
Accept-Language: en-US,en;q=0.9
```

Indicates the language preferences sent by the browser.

### 9. Interpret the Results

The procedure demonstrates the basic operation of a honeypot, which can simulate an available service and record interactions with it.

The laboratory flow can be represented as follows:

```text
Windows Server 2022
        |
        | HTTP request
        v
192.168.98.40:80
        |
        v
PentBox Honeypot
        |
        v
Recorded request in the Kali Linux terminal
```

PentBox detected the access attempt and displayed HTTP request information in the terminal.

The record made it possible to observe:

- Source IP address.
- Source port.
- HTTP method.
- Requested path.
- Destination host.
- Browser information reported by the client.
- Operating system information included in the User-Agent string.
- Accepted content types.
- Accepted compression methods.
- Language preferences provided by the client.

The label `INTRUSION ATTEMPT DETECTED!` is the tool's alert wording. In this exercise, the observed activity was a request made by the authorized laboratory client; the label alone does not prove malicious intent.

## Concepts Practiced

### Honeypot

A honeypot is a resource designed to attract, observe, and record interactions that may be unexpected within a particular service or environment.

In security operations, such records can support the detection and analysis of suspicious behavior.

### PentBox

PentBox is a collection of tools for security and network testing. This activity specifically used its honeypot module.

### HTTP

HTTP is used for communication between clients, such as web browsers, and web servers.

The activity allowed an HTTP request generated by a browser to be observed directly.

### Logs and Indicators

The PentBox output demonstrates how connection information can be recorded and used as evidence during network-event analysis.

### Source IP and Port

The source IP and port help identify the network endpoint from which the connection was observed. These values are useful for investigation but do not, on their own, establish the identity of a person or device beyond the laboratory context.

## Commands and Tools Used

The following commands were used during the activity:

```bash
sudo -i
ifconfig
cd /curso/pentbox/pentbox-1.8
./pentbox.rb
```

The browser test was performed from Windows Server 2022 using:

```text
http://192.168.98.40
```

## Results

The honeypot was configured on Kali Linux using PentBox and activated on TCP port `80`.

A request was sent from Windows Server 2022 to the Kali Linux address. PentBox detected the interaction and recorded the HTTP request in the terminal.

The activity provided practical experience with:

- Configuring a honeypot.
- Using a TCP listening service.
- Generating an HTTP request from another system.
- Identifying the source connection information.
- Analyzing HTTP headers.
- Observing browser-supplied information in security logs.

The laboratory demonstrated how a honeypot can record network interactions for observation and analysis in a controlled environment.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 11–12.

**Recorded screenshot:** Step 10 of the activity, showing the access attempt recorded by the honeypot in the Kali Linux terminal.

[View Evidence — Classes 11–12](../evidencias.pdf)

---

[Back to Classes 11–12](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
