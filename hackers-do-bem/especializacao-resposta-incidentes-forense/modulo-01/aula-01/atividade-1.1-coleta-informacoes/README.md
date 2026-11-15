# Activity 1.1 — Information Gathering with Python Sockets

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Documented

## Objective

Build a basic client-server application using Python sockets to understand network communication and identify services listening on a specific port.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Programming Language | Python 3 |
| Library | socket |
| Server Port | 12345 |
| Communication | TCP |

## Procedure

### 1. Create the Server

Open the terminal editor:

```bash
nano servidor.py
```

The server program creates a socket, binds it to the local hostname and port 12345, and starts listening for incoming connections.

Main methods used:

- `socket.socket()` — creates the socket.
- `bind()` — associates the socket with an address and port.
- `listen()` — enables incoming connection handling.
- `accept()` — accepts a client connection.
- `send()` — sends a message to the connected client.
- `close()` — closes the connection.

### 2. Create the Client

Create the client program:

```bash
nano cliente.py
```

The client creates a TCP socket and connects to the server on port 12345.

Methods used:

- `connect()` — establishes the connection.
- `recv()` — receives data from the server.
- `close()` — closes the connection.

### 3. Execute the Server

Start the server:

```bash
python3 servidor.py
```

The expected initial message is:

```text
socket esta na escuta
```

### 4. Execute the Client

Open a second terminal and execute:

```bash
python3 cliente.py
```

The client receives the server confirmation message:

```text
Conexao estabelecida
```

The server also records information about the incoming connection.

## Technical Analysis

The assignment description refers to UDP and an Echo Server. However, the supplied implementation uses TCP:

- The server uses `socket.socket()` with the default stream socket type.
- The client explicitly uses `socket.SOCK_STREAM`.
- The server sends a fixed confirmation message rather than receiving and echoing client data.

Therefore, the implemented exercise demonstrates TCP client-server communication, not UDP echo communication.

## Result

The activity demonstrates how to create a listening server, establish a client connection, exchange a message, and close a network connection.

## Concepts Practiced

- Python socket programming
- TCP communication
- Server and client architecture
- Network ports and listening services
- Connection handling
- Basic network information gathering

## Evidence

[Activity 1.1 — PDF Evidence](./1.1.pdf)

---

[Back to Class 01](../README.md) · [Back to Specialization](../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
