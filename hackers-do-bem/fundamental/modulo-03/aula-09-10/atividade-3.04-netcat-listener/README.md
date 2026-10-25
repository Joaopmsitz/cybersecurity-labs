# Activity 3.04 — Creating a TCP Listener with Netcat

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 09–10  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use Netcat (`nc`) to create a TCP listener on a specific port and observe an HTTP request sent by a web browser.

The activity demonstrates how a simple networking tool can accept TCP connections and display the data transmitted by a client.

## Environment

- **Operating system:** Kali Linux
- **Tool:** Netcat
- **Browser:** Mozilla Firefox
- **Network interface:** `eth0`
- **Kali Linux IP address:** `192.168.98.40`
- **Port:** `5555`
- **Protocol observed:** HTTP

## Procedure

### 1. Obtain Root Access

Administrative access was obtained using:

```bash id="b8d3vu"
sudo -i
```

This opened a root shell for the laboratory procedures.

### 2. Review the Netcat Help Output

The following command was used to inspect the available options in the installed Netcat version:

```bash id="a3n4wa"
nc -help
```

**Observed output:**

```text id="f5sd69"
OpenBSD netcat (Debian patchlevel 1.229-1)
usage: nc [-46CDdFhklNnrStUuvZz] [-I length] [-i interval] [-M ttl]
          [-m minttl] [-O length] [-P proxy_username] [-p source_port]
          [-q seconds] [-s sourceaddr] [-T toskeyword] [-V rtable]
          [-w timeout] [-X proxy_protocol] [-x proxy_address[:port]]
          [destination] [port]

Command Summary:
-4              Use IPv4
-6              Use IPv6
-C              Send CRLF as line-ending
-D              Enable debugging
-d              Detach from stdin
-F              Pass socket fd
-h              Display this help text
-k              Keep inbound sockets open for multiple connections
-l              Listen for inbound rather than outbound connections
-N              Shutdown the network socket after EOF on stdin
-n              Suppress name/port resolutions
-r              Randomize remote ports
-S              Enable the TCP MD5 signature option
-s sourceaddr   Local source address
-t              Answer TELNET negotiation
-U              Use UNIX domain socket
-u              UDP mode
-v              Verbose
-w timeout      Timeout for connects and final net reads
-X proxy_protocol
-x proxy_address[:port]
-z              Zero-I/O mode
```

The options most relevant to this activity were:

- `-l` — places Netcat in listening mode.
- `-p` — specifies the local port to use.
- `-v` — enables verbose connection information.

The installed version was OpenBSD Netcat, as indicated in the output.

### 3. Identify the IP Address

The network interfaces were inspected using:

```bash id="35gxyv"
ifconfig
```

The interface used in the laboratory was `eth0`, configured with the address:

```text id="fy4nqv"
192.168.98.40
```

The interface belonged to the following network:

```text id="kaf35w"
192.168.98.0/24
```

This address was used to access the listener from Firefox.

### 4. Create the Listener

A TCP listener was started on port `5555`:

```bash id="fv4e3i"
nc -l -p 5555 -v
```

Netcat displayed:

```text id="b8z7ef"
listening on [any] 5555 ...
```

At this point, Netcat remained waiting for an incoming connection on port `5555`.

The command options can be understood as follows:

- `-l` — listen for incoming connections.
- `-p` — use the specified port.
- `-v` — display detailed connection information.

### 5. Connect Through the Browser

With the listener running, Firefox was opened and the following URL was accessed:

```text id="wqj0dz"
http://192.168.98.40:5555
```

The browser attempted to establish a TCP connection to port `5555` on the Kali Linux machine.

Because Netcat was listening on that port, the connection was received by the Netcat process.

The browser then sent an HTTP request to the listener.

### 6. Observe the HTTP Request

The following output was observed in the Netcat terminal:

```text id="g9f4v2"
┌──(root㉿kali)-[~]
└─# nc -l -p 5555 -v
Listening on 0.0.0.0 5555
Connection received on ip-192-168-98-40.ec2.internal 42396
GET / HTTP/1.1
Host: 192.168.98.40:5555
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```

This was the main result of the activity.

Netcat accepted the connection and displayed the data sent by the browser directly in the terminal.

The output includes the client-side source port `42396`, which was used for this connection, and the HTTP request headers sent by Firefox.

#### Interpreting the Request

**Request line**

```http
GET / HTTP/1.1
```

This line indicates an HTTP request using the `GET` method to request the `/` resource over HTTP/1.1.

**Host**

```http
Host: 192.168.98.40:5555
```

Identifies the destination host and the port used for the request.

**User-Agent**

```http
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
```

Provides information about the client making the request. In this case, the request was generated by Firefox running on Linux.

**Accept**

```http
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

Indicates the types of content the browser is willing to accept in a response, along with their relative preferences.

**Accept-Language**

```http
Accept-Language: en-US,en;q=0.5
```

Indicates the language preferences supplied by the browser.

**Accept-Encoding**

```http
Accept-Encoding: gzip, deflate
```

Lists compression formats accepted by the client for the response.

**Connection**

```http
Connection: keep-alive
```

Indicates the client's preference to keep the TCP connection available for further communication.

**Upgrade-Insecure-Requests**

```http
Upgrade-Insecure-Requests: 1
```

Indicates that the browser expresses a preference for upgrading insecure requests to secure connections when supported by the destination and browser behavior.

**Priority**

```http
Priority: u=0, i
```

Provides request-priority information using the priority syntax supported by the client.

The captured request demonstrates that an HTTP request contains a request line and headers that provide additional information about the client and destination.

## Concepts Practiced

### Netcat

Netcat is a networking utility used to establish TCP/UDP connections, create listeners, and test network communication.

### Listener

A listener is a process that waits for incoming connections on a specified address and port.

In this laboratory, the listener used:

- **IP address:** `192.168.98.40`
- **Port:** `5555`

### TCP

The browser established a TCP connection to Netcat, allowing the process to receive data sent by the client.

TCP provides a connection-oriented transport mechanism, while the application data in this exercise followed the HTTP protocol.

### HTTP

The observed request used HTTP, allowing its request line and headers to be viewed directly in the terminal.

Because the request used plain HTTP rather than HTTPS, the request data was visible to the listener without TLS decryption.

### HTTP Headers

The captured headers demonstrated that HTTP requests contain information beyond the method and requested path.

The headers observed included:

- `Host`
- `User-Agent`
- `Accept`
- `Accept-Language`
- `Accept-Encoding`
- `Connection`
- `Upgrade-Insecure-Requests`
- `Priority`

These fields help describe the request and the client's preferences.

## Commands Used

The commands used during the activity were:

```bash id="c5s8d7"
sudo -i
nc -help
ifconfig
nc -l -p 5555 -v
```

The listener was accessed through Firefox using:

```text id="c1p4nu"
http://192.168.98.40:5555
```

## Results

The activity demonstrated how Netcat can create a TCP listener and receive an HTTP request directly from a web browser.

Firefox connected to:

```text id="e3ud8v"
192.168.98.40:5555
```

Netcat received the connection and displayed the following information in the terminal:

- The incoming connection.
- The client's source port.
- The HTTP method.
- The requested path.
- The HTTP protocol version.
- The headers sent by the browser.

The exercise helped connect concepts involving TCP, ports, listeners, network connections, and HTTP request structure.

The listener acted as a simple demonstration endpoint; the activity did not establish a complete web server or generate a full HTTP response.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 09–10.

**Recorded screenshot:** Step 6 of the activity, as required by the laboratory instructions.

[View Evidence — Classes 09–10](../evidencias.pdf)

---

[Back to Classes 09–10](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
