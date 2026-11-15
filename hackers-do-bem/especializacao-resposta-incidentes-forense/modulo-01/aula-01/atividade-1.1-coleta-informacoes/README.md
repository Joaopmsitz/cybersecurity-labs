# Activity 1.1 — Information Gathering with Python Sockets

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Develop a basic server and client application using Python sockets to understand network communication and identify services listening on a specific port.

The exercise introduces information gathering as an initial stage of incident response and security assessment.

During reconnaissance, security professionals collect information about the target environment, including IP addresses, operating systems, installed software, and listening services.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Access | RDP through landing |
| VM Address | 192.168.98.10 |
| Programming Language | Python 3 |
| Python Library | socket |
| Server Port | 12345 |
| Transport Protocol | TCP |
| Server File | servidor.py |
| Client File | cliente.py |

## 3. Network Socket Concepts

A socket represents an endpoint used by an application to send and receive data over a network.

The exercise uses the Python `socket` library.

The server uses the following operations:

| Method | Function |
|---|---|
| `socket.socket()` | Creates a socket object |
| `gethostname()` | Retrieves the local hostname |
| `bind()` | Associates the socket with a local address and port |
| `listen()` | Places the socket in listening mode |
| `accept()` | Accepts an incoming connection |
| `send()` | Sends data through the established connection |
| `close()` | Closes the socket connection |

The client uses:

| Method | Function |
|---|---|
| `socket.socket()` | Creates the client socket |
| `connect()` | Establishes a connection with the server |
| `recv()` | Receives data from the server |
| `close()` | Closes the client connection |
| `decode()` | Converts received bytes into a string |

## 4. Procedure

### Step 1 — Create the Server File

Open the Nano editor:

```bash
nano servidor.py
```

### Step 2 — Implement the Server

Insert the following code:

```python
import socket

def Main():
    _host_ = socket.gethostname()
    port = 12345

    serversocket = socket.socket()
    serversocket.bind((_host_, port))
    serversocket.listen(1)

    print('socket esta na escuta')

    while True:
        conn, addr = serversocket.accept()

        print("Recebido conexao de %s" % str(addr))

        msg = 'Conexao estabelecida' + "\r\n"
        conn.send(msg.encode('ascii'))

        conn.close()


if __name__ == '__main__':
    Main()
```

### Step 3 — Create the Client File

Open a second script:

```bash
nano cliente.py
```

Insert:

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

_host_ = socket.gethostname()
port = 12345

s.connect((_host_, port))

msg = s.recv(1024)

s.close()

print(msg.decode('ascii'))
```

### Step 4 — Start the Server

Execute:

```bash
python3 servidor.py
```

Expected initial output:

```text
socket esta na escuta
```

Keep the server running.

### Step 5 — Execute the Client

Open another terminal and execute:

```bash
python3 cliente.py
```

The expected client output is:

```text
Conexao estabelecida
```

### Step 6 — Observe the Server Connection

The server accepts the incoming connection and reports the connecting client's address.

Expected output structure:

```text
socket esta na escuta
Recebido conexao de ('<client-ip>', <client-port>)
```

The IP address and temporary client port depend on the execution environment.

### Step 7 — Capture the Server Output

Return to the server terminal and capture the output, including the command execution and connection information.

Before taking the screenshot, configure the terminal prompt using the alias specified by the assignment.

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\u/meunome/g')"
```

Replace `meunome` with the appropriate alias.

## 5. Expected Results

The server waits for connections on port 12345.

After the client connects, the server prints the remote address and sends a confirmation message.

The client receives and displays:

```text
Conexao estabelecida
```

## 6. Technical Analysis

### TCP Instead of UDP

The assignment description refers to an Echo Server using UDP. However, the supplied source code implements TCP.

The reason is the socket type:

```python
socket.socket()
```

The default Python socket parameters use:

- Address family: `AF_INET`
- Socket type: `SOCK_STREAM`

The client also explicitly specifies:

```python
socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

`SOCK_STREAM` is associated with TCP stream communication.

UDP would normally use `SOCK_DGRAM`.

### Why This Is Not a True Echo Server

A conventional Echo Server receives data from a client and sends that same data back.

The provided server instead sends a fixed message:

```python
msg = 'Conexao estabelecida' + "\r\n"
conn.send(msg.encode('ascii'))
```

It does not call `recv()` to read client-provided content.

Therefore, the exercise demonstrates TCP connection establishment and a fixed server response, rather than UDP echo behavior.

### Listening Backlog

The following instruction:

```python
serversocket.listen(1)
```

sets the requested backlog for pending connection requests.

It should not be interpreted as a guarantee that the server can maintain only one client connection at a time.

## 7. Results and Interpretation

The activity demonstrates the relationship between a listening network service and its connecting client.

The server remains available while the Python process is running and accepts incoming TCP connection requests.

This type of communication provides a basic foundation for understanding exposed services and network information gathering.

## 8. Concepts Practiced

- Python network programming
- TCP stream sockets
- Client-server architecture
- Socket binding
- Listening ports
- Connection acceptance
- Data transmission
- Connection closure
- Network reconnaissance

## 9. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The required evidence corresponds to Step 7, showing the server terminal and the accepted client connection.

## References

- [Python Socket Documentation](https://docs.python.org/3/library/socket.html)
- [Python Socket Programming HOWTO](https://docs.python.org/3/howto/sockets.html)

---

[Back to Class 01](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
