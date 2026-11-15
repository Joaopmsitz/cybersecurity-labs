# Activity 1.4 — DNS Reconnaissance and Nmap Scanning

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Understand DNS resolution, reverse DNS lookups, and network reconnaissance using Nmap.

The activity introduces the relationship between domain names and IP addresses and demonstrates how Nmap identifies exposed ports.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| DNS Tools | nslookup, dig |
| Network Scanner | Nmap |
| Target Domain | scanme.nmap.org |
| Example IPv4 | 45.33.32.156 |

## 3. DNS Reconnaissance

DNS translates human-readable domain names into network addresses.

A forward DNS lookup identifies the IP addresses associated with a hostname.

A reverse DNS lookup attempts to identify a hostname associated with an IP address.

## 4. Procedure

### Step 1 — Perform Forward DNS Resolution

Execute:

```bash
nslookup scanme.nmap.org
```

Example output supplied in the training material:

```text
Server: 10.0.2.3
Address: 10.0.2.3#53

Non-authoritative answer:
Name: scanme.nmap.org
Address: 45.33.32.156
Name: scanme.nmap.org
Address: 2600:3c01::f03c:91ff:fe18:bb2f
```

The response contains:

- DNS server address.
- DNS server port 53.
- Hostname queried.
- IPv4 address.
- IPv6 address.

The `Non-authoritative answer` label indicates that the response was supplied by a DNS resolver rather than directly by the domain's authoritative name server.

The addresses shown are historical example values from the assignment and may change over time.

### Alternative Command

If `nslookup` is unavailable:

```bash
dig scanme.nmap.org
```

If the DNS utilities are missing, the assignment provides:

```bash
sudo apt update
sudo apt install dnsutils
```

Then retry:

```bash
nslookup scanme.nmap.org
```

### Step 2 — Perform Reverse DNS Lookup

Execute:

```bash
nslookup 45.33.32.156
```

Example output:

```text
156.32.33.45.in-addr.arpa name = scanme.nmap.org.

Authoritative answers can be found from:

32.33.45.in-addr.arpa nameserver = ns5.linode.com.
32.33.45.in-addr.arpa nameserver = ns3.linode.com.
32.33.45.in-addr.arpa nameserver = ns1.linode.com.
32.33.45.in-addr.arpa nameserver = ns2.linode.com.
32.33.45.in-addr.arpa nameserver = ns4.linode.com.
```

The reverse lookup uses the reverse DNS namespace:

```text
in-addr.arpa
```

IPv4 addresses are represented in reverse order for PTR record queries.

### Step 3 — Execute Nmap Scan

Run:

```bash
nmap scanme.nmap.org -vv
```

The `-vv` option increases the output verbosity.

The scan can provide information such as:

- Target host status.
- Ports examined.
- Open ports.
- Closed or filtered ports.
- Associated service information.
- Scan completion information.

The exact scan output is dependent on the target and the network conditions at execution time.

## 5. Nmap Command Analysis

The command:

```bash
nmap scanme.nmap.org -vv
```

contains:

| Argument | Meaning |
|---|---|
| `nmap` | Runs the Nmap scanner |
| `scanme.nmap.org` | Target hostname |
| `-vv` | Requests a higher verbosity level |

Nmap recognizes several port states:

| State | Meaning |
|---|---|
| open | An application is accepting connections |
| closed | The port is reachable, but no application is listening |
| filtered | Filtering prevents Nmap from determining whether the port is open |
| unfiltered | The port is accessible, but its open or closed status is not established |
| open\|filtered | Nmap cannot distinguish between open and filtered |
| closed\|filtered | Nmap cannot distinguish between closed and filtered |

## 6. Technical Interpretation

DNS reconnaissance provides information needed to identify the infrastructure associated with a domain.

Combining forward and reverse lookups provides additional context about the target.

Nmap extends that information by investigating accessible ports.

An open port can indicate a listening service, but additional enumeration is required to identify the application and determine whether any security weakness exists.

## 7. Authorization and Responsible Use

The training material identifies scanme.nmap.org as a test host.

Nmap's official scanning policy permits limited testing of that host and prohibits exploit testing or denial-of-service activity.

The official guidance also requests that users limit the frequency of scans.

For any other system, obtain explicit authorization before performing reconnaissance.

## 8. Results

The activity demonstrates:

- Forward DNS resolution.
- Reverse DNS resolution.
- IP address interpretation.
- Detailed network scanning using Nmap.

The DNS outputs above are examples supplied by the original material.

No full Nmap output was preserved in the available student notes, so scan-specific port states are not fabricated.

## 9. Concepts Practiced

- DNS
- IPv4 and IPv6
- Reverse DNS
- PTR records
- Network reconnaissance
- Nmap
- Port states
- Verbose scanning
- Authorized security testing

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

Required screenshot: Step 3, showing the Nmap command and its output.

## References

- [Nmap Documentation](https://nmap.org/book/)
- [Nmap Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html)
- [Nmap Verbosity Options](https://nmap.org/book/port-scanning-options.html)
- [Python DNS Tools — General Concepts](https://docs.python.org/3/library/socket.html)

---

[Back to Class 01](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
