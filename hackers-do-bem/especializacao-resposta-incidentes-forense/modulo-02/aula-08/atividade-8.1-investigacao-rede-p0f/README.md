# Activity 8.1 - Network Investigation with p0f

## Overview

This activity uses p0f to passively identify operating system characteristics from observed network traffic. WHOIS is then used to investigate an IP address observed by p0f.

## Objectives

- Inspect p0f command-line options.
- Identify available network interfaces.
- Monitor traffic using passive OS fingerprinting.
- Investigate an observed IP address using WHOIS.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Network Interface | `ens5` |
| Fingerprinting Tool | p0f |
| Lookup Tool | WHOIS |

## Procedure

### 1. Inspect p0f

Locate the p0f executable:

```bash
whereis p0f
```

Inspect the available options:

```bash
/usr/sbin/p0f -h
```

The options displayed depend on the installed p0f build. Consult its manual if the help flag behaves differently.

### 2. Identify Network Interfaces

Use:

```bash
ip addr
```

Alternatively:

```bash
/sbin/ifconfig
```

The practical activity uses the `ens5` Ethernet interface.

### 3. Start Passive Fingerprinting

Run p0f on the selected interface:

```bash
sudo /usr/sbin/p0f -i ens5
```

Keep the process running while generating normal browser traffic.

### 4. Generate Network Activity

Open a web browser and visit the training examples:

- https://www.cfsi.co/
- https://www.offsec.com/

Observe the connections reported by p0f.

The training material includes example operating system fingerprints such as Linux 2.2.x-3.x. Actual results depend on the traffic and fingerprint database.

### 5. Investigate an Observed IP Address

Choose an IP address displayed by the running p0f process.

Open a second terminal and query the selected address:

```bash
whois <OBSERVED_IP> | more
```

Replace `<OBSERVED_IP>` with an address actually observed in the p0f output.

## Expected Result

p0f displays passive connection and operating system fingerprint information from observed traffic. WHOIS provides registration and network ownership information about the selected IP address.

## Evidence

**Required screenshot: Step 8 - Print 1, PDF page 1.**

The screenshot must show two terminal windows side by side:

- The first terminal displays the p0f process running on `ens5`.
- The second terminal displays the WHOIS query and its output for an IP address observed by p0f.

Configure the terminal prompt as required by the course before capturing terminal evidence:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\\u/meunome/g')"
```

Replace `meunome` with the required student alias.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- p0f performs passive fingerprinting by observing traffic.
- The results depend on the packets visible to the selected interface.
- WHOIS information may identify the organization or network allocation associated with an address, but does not necessarily identify the exact device or user.
- The example IP addresses in the course are illustrative. Use an address observed during the practical exercise.

## References

- [Kali Linux - p0f](https://www.kali.org/tools/p0f/)

## Navigation

- [Class 08](../README.md)
- [Module 02](../../README.md)
- [Next Activity - 8.2](../atividade-8.2-pos-exploracao-bashark/README.md)
