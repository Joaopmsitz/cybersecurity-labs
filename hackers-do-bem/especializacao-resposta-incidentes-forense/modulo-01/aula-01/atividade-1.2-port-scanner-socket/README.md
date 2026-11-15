# Activity 1.2 — TCP Port Scanner using Python Sockets

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Develop a basic TCP port scanner using Python sockets to identify open ports on a target host.

Port scanning is an important reconnaissance technique because it helps identify services that may be exposed to a network.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Language | Python 3 |
| Library | socket |
| Additional Module | time |
| Target Host | scanme.nmap.org |
| Target IPv4 in Exercise | 45.33.32.156 |
| Port Range | 70–80 |
| Transport Protocol | TCP |

## 3. Port Classification

The original assignment groups TCP/IP ports into three main ranges:

| Range | Classification |
|---|---|
| 0–1023 | System or well-known ports |
| 1024–49151 | Registered or user ports |
| 49152–65535 | Dynamic or private ports |

A port can provide information about services that may be available on a system.

The presence of an open port does not, by itself, establish that a system is vulnerable.

## 4. Procedure

### Step 1 — Create the Script

Open Nano:

```bash
nano atividade2.py
```

### Step 2 — Implement the Port Scanner

Insert:

```python
from socket import *
import time

startTime = time.time()

if __name__ == '__main__':

    print('_host_ a ser escaneado: 45.33.32.156')
    print('Pressione enter')
    input()

    target = '45.33.32.156'
    t_IP = gethostbyname(target)

    print('Iniciando varredura no _host_: ', t_IP)

    for i in range(70, 81):

        s = socket(AF_INET, SOCK_STREAM)

        conn = s.connect_ex((t_IP, i))

        if conn == 0:
            print('Porta %d: OPEN' % (i,))

        s.close()

    print('Time taken:', time.time() - startTime)
```

### Step 3 — Execute the Scanner

Run:

```bash
python3 atividade2.py
```

Press Enter when requested.

The script resolves the target address and attempts TCP connections against each port in the configured interval.

## 5. Expected Output

The training material describes the following expected discovery:

```text
_host_ a ser escaneado: 45.33.32.156
Pressione enter

Iniciando varredura no _host_: 45.33.32.156
Porta 80: OPEN
Time taken: <execution-time>
```

The exact execution time and scan output depend on the target's current response and network conditions.

The port 80 result above is the expected result described in the original assignment, not a live scan verification.

## 6. Code Analysis

### Target Resolution

```python
target = '45.33.32.156'
t_IP = gethostbyname(target)
```

The hostname resolution function translates a hostname into an IP address.

The assignment uses the IP address associated with scanme.nmap.org.

### TCP Socket Creation

```python
s = socket(AF_INET, SOCK_STREAM)
```

The scanner creates an IPv4 TCP socket.

### Connection Testing

```python
conn = s.connect_ex((t_IP, i))
```

`connect_ex()` attempts to establish a connection and returns an error indicator.

A return value of `0` indicates a successful connection.

### Port Detection

```python
if conn == 0:
    print('Porta %d: OPEN' % (i,))
```

A successful TCP connection is reported as an open port.

### Port Interval

```python
for i in range(70, 81):
```

Python's `range()` excludes its upper boundary.

Therefore, this scanner tests:

```text
70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80
```

The actual interval contains eleven ports.

### Execution Time

```python
startTime = time.time()
```

and:

```python
print('Time taken:', time.time() - startTime)
```

The code measures the elapsed execution time.

## 7. Technical Interpretation

The scanner performs sequential TCP connection attempts.

A port is reported as `OPEN` when the target accepts the connection attempt.

Other connection results are not displayed by the supplied implementation.

For a more complete assessment, additional information such as service identification, network filtering, and application behavior would be needed.

## 8. Authorization and Responsible Use

The exercise identifies scanme.nmap.org as a service maintained for learning and testing Nmap.

Nmap's official guidance permits scanning this host subject to its stated limits. The official page also discourages exploit testing and denial-of-service activities.

Port scanning must only be performed against systems for which appropriate authorization exists.

## 9. Concepts Practiced

- Python socket programming
- IPv4 TCP connectivity
- Port scanning
- Hostname and IP resolution
- `connect_ex()`
- Open port identification
- Execution time measurement
- Authorized reconnaissance

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

Required screenshot: Step 3, showing the script execution and the reported port scan output.

## References

- [Python Socket Documentation](https://docs.python.org/3/library/socket.html)
- [Nmap Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html)
- [Nmap Scanme Legal Information](https://nmap.org/book/legal-issues.html)

---

[Back to Class 01](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
