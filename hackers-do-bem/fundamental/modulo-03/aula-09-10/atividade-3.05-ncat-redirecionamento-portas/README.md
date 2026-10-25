# Activity 3.05 — Port Forwarding Concepts with Ncat

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 03  
> **Class:** 09–10  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use Ncat, a networking utility included in the Nmap project, to observe how data can be passed between TCP connections using different ports.

The activity demonstrates how Ncat can create listeners and establish connections between them in a controlled laboratory environment.

**Important distinction:** The procedure uses an intermediate connection involving ports 80 and 443. It does not, by itself, implement conventional transparent port forwarding or network address translation (NAT). The purpose is to observe the flow of data between connections created by Ncat.

## Environment

- **Operating system:** Kali Linux
- **Tool:** Ncat 7.95
- **Initial listener port:** `80`
- **Second listener port:** `443`
- **Address used for testing:** `127.0.0.1`
- **Terminals used:** Three

## Procedure

### 1. Obtain Root Access

Administrative access was obtained using:

```bash id="7f5g2b"
sudo -i
```

This opened a root shell for the laboratory procedure.

### 2. Create a Listener on Port 80

In the first terminal, the following command was executed:

```bash id="x2s1pg"
ncat -vl 80 -c 'ncat -l 443'
```

The observed output was:

```text id="g8y5qh"
Ncat: Version 7.95 ( https://nmap.org/ncat )
Ncat: Listening on [::]:80
Ncat: Listening on 0.0.0.0:80
```

The command uses the following options and arguments:

- `-v` — enables verbose output.
- `-l` — enables listening mode.
- `80` — specifies the port used by the first listener.
- `-c` — executes a command when a connection is received.
- `ncat -l 443` — starts a second Ncat listener on port 443.

The first Ncat process waits for incoming connections on port 80. When a connection is accepted, the command specified with `-c` starts another Ncat process that listens on port 443.

**Security note:** The output shows that the first listener is bound to `0.0.0.0` and `[::]`, which normally means listening on all available IPv4 and IPv6 interfaces, respectively. Although the test connections used the loopback address, this listener configuration may expose the service to other devices on the network. Such experiments should be performed only in an authorized, isolated environment, and the listeners should be stopped when the test is complete.

### 3. Connect to Port 80

In the second terminal, a connection was established to the previously created listener:

```bash id="wh5d2b"
ncat -nv 127.0.0.1 80
```

The connection was established with the local listener.

In the first terminal, the incoming connection was displayed:

```text id="q8br1f"
Ncat: Connection from 127.0.0.1:59584.
```

At this point, the first Ncat process had received a connection from the second terminal. The source port shown in the output was `59584`.

### 4. Connect to Port 443

In the third terminal, a connection was made to port 443:

```bash id="mb9v6t"
ncat -v 127.0.0.1 443
```

Ncat confirmed the connection to the second listener:

```text id="k7p3xw"
Ncat: Connected to 127.0.0.1:443.
```

The two client connections and the Ncat processes were arranged as follows:

```text id="s8x4qw"
Terminal 2
    |
    | TCP connection to port 80
    v
Ncat listener on port 80
    |
    | Executes a second Ncat process
    v
Ncat listener on port 443
    ^
    | TCP connection to port 443
    |
Terminal 3
```

The first listener starts the second Ncat process when it receives a connection. The second Ncat process then accepts a separate connection on port 443. Because the child process is connected to the first Ncat session through its input and output streams, it can pass data between the two connections.

### 5. Test Data Transmission

With the connections established, a simple data transmission test was performed.

In the third terminal, the following text was entered:

```text id="vy4rt6"
Teste A
```

The text was received in the second terminal:

```text id="rw7a5g"
Teste A
```

Next, the following text was entered in the second terminal:

```text id="az9b4w"
Teste B
```

The text was received in the third terminal:

```text id="jq3v6z"
Teste B
```

This behavior demonstrated that data sent from either endpoint could be observed at the other endpoint through the connections established by Ncat.

### 6. Interpret the Procedure

The main command was:

```bash id="xdq4pr"
ncat -vl 80 -c 'ncat -l 443'
```

It creates a listener on port 80. When a connection is received, the `-c` option causes another Ncat process to be started:

```bash id="j7m2ve"
ncat -l 443
```

The second Ncat process creates a listener on port 443.

The exercise uses these listeners to demonstrate how TCP connections can be established and how data can flow between the terminals through the connected Ncat processes.

This behavior should be distinguished from transparent port forwarding performed by mechanisms such as NAT or firewall rules. In this laboratory, communication depends on the Ncat processes launched by the command.

## Concepts Practiced

### Ncat

Ncat is a network communication utility included in the Nmap project. It can create listeners, establish TCP/UDP connections, and test communications between hosts and ports.

### Listener

A listener waits for incoming connections on a specified port.

The laboratory used listeners on:

```text id="bn8k3a"
80
443
```

### Loopback Address

The address:

```text id="x5m2za"
127.0.0.1
```

refers to the local machine. Both client connections in this exercise targeted the local host, even though the listener itself was configured to bind to all available interfaces.

### TCP Ports

Ports 80 and 443 are traditionally associated with HTTP and HTTPS, respectively. In this exercise, however, they were used as TCP ports to demonstrate Ncat connections and data transfer. Using port 443 does not automatically provide HTTPS or TLS encryption.

### `-l`

Enables Ncat listening mode:

```bash id="d8v3zx"
-l
```

This causes Ncat to wait for incoming connections.

### `-v`

Enables verbose output:

```bash id="m6z5an"
-v
```

This allows connection details to be displayed.

### `-c`

Executes a command when a connection is received:

```bash id="e9y2wq"
-c
```

In this laboratory, it was used to launch the second Ncat listener.

### Data Forwarding Between Connections

The child Ncat process receives input and output from the parent connection while accepting another TCP connection. This arrangement allows the two connected endpoints to exchange data through the processes.

It is a demonstration of data relaying using Ncat, rather than a general-purpose transparent network forwarding configuration.

## Commands Used

The commands used during the activity were:

```bash id="g7h2pv"
sudo -i
ncat -vl 80 -c 'ncat -l 443'
ncat -nv 127.0.0.1 80
ncat -v 127.0.0.1 443
```

The test messages were:

```text id="u4h8cs"
Teste A
Teste B
```

## Results

The activity demonstrated how to create Ncat listeners and establish TCP connections between different terminals.

The procedure covered:

- Creating a listener on port 80.
- Receiving a local TCP connection.
- Executing a second Ncat process that listens on port 443.
- Establishing a second TCP connection.
- Transmitting data between the two endpoints.
- Observing the messages sent and received in each terminal.
- Understanding the difference between relaying data through Ncat and transparent port forwarding.

The `Teste A` and `Teste B` messages confirmed that communication between the endpoints worked during the laboratory exercise.

## Evidence

The activity evidence is included in the PDF for Module 03, Classes 09–10.

**Recorded screenshot:** Step 9 of the activity, as required by the laboratory instructions.

[View Evidence — Classes 09–10](../evidencias.pdf)

---

[Back to Classes 09–10](../) · [Back to Module 03](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
