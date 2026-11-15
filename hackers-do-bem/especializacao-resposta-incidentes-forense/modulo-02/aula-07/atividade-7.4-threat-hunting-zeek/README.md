# Activity 7.4 - Threat Hunting with Zeek

## Overview

This activity uses Zeek to extract metadata from PCAP files and investigate network behavior. The practical work focuses on connection records, top talkers, protocols, HTTP metadata, transferred files, and DNS queries.

## Objectives

- Generate Zeek logs from a PCAP file.
- Extract network connection fields using `zeek-cut`.
- Identify hosts and traffic volumes.
- Investigate protocol and application metadata.
- Examine DNS queries for potentially suspicious domains.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Network Monitor | Zeek |
| PCAP Directory | `/opt/zeek/analise_pcap` |
| Main Log | `conn.log` |
| Log Extraction Tool | `zeek-cut` |

## Procedure

### 1. Generate Zeek Logs from a PCAP

Move to the analysis directory:

```bash
cd /opt/zeek/analise_pcap
```

Process the provided capture:

```bash
sudo /opt/zeek/bin/zeek -Cr /opt/zeek/analise_pcap/arquivo_mesclado1.pcap
```

List the generated logs:

```bash
ls -l *.log
```

The `-r` option reads the PCAP file offline. The `-C` option disables checksum validation.

### 2. Extract Connection Metadata

Use `zeek-cut` to extract source and destination addresses, transferred bytes, and packet counts:

```bash
cat /opt/zeek/analise_pcap/conn.log | zeek-cut id.orig_h id.resp_h orig_bytes resp_bytes orig_pkts resp_pkts
```

To sort the output by the original byte count:

```bash
cat /opt/zeek/analise_pcap/conn.log | zeek-cut id.orig_h id.resp_h orig_bytes resp_bytes orig_pkts resp_pkts | sort -k3 -nr | more
```

### 3. Investigate Other Log Types

Identify network services:

```bash
cat /opt/zeek/analise_pcap/conn.log | zeek-cut -d ts id.orig_h id.resp_h service | awk '{if($4 != "dns" && $4 != "-") print $1,$2,$3,$4}'
```

Inspect HTTP referrers:

```bash
cat /opt/zeek/analise_pcap/http.log | zeek-cut id.orig_h id.resp_h host referrer
```

Review HTTP hosts, referrers, and requested URIs:

```bash
cat /opt/zeek/analise_pcap/http.log | zeek-cut -d ts id.orig_h id.resp_h host referrer uri
```

Inspect files transferred over the network:

```bash
cat /opt/zeek/analise_pcap/files.log | zeek-cut -d ts tx_hosts rx_hosts source mime_type filename
```

### 4. Investigate DNS Queries

Filter common domains from DNS query logs for further investigation:

```bash
sudo su
cat /opt/zeek/analise_pcap/dns.log | zeek-cut -d ts id.orig_h id.resp_h query | grep -Ev '(microsoft|akamai|google|windowsupdate|msft|apple|comanyname)' > /opt/zeek/analise_pcap/dns_queries.txt
exit
```

Search compressed log files for a specific domain:

```bash
zgrep qsertopinajil.com /opt/zeek/analise_pcap/*
```

## Expected Result

Zeek generates structured logs from the PCAP file. The `zeek-cut` output exposes relevant connection metadata for traffic analysis and threat hunting.

## Evidence

**Required screenshot: Step 3 - Print 9, PDF page 4.**

The terminal must show the `zeek-cut` command and its output containing source IP, destination IP, and traffic volume fields.

Configure the terminal prompt as required by the course before capturing the terminal evidence:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\\u/meunome/g')"
```

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- `conn.log` records TCP, UDP, and ICMP connection information.
- `http.log` contains HTTP request and response metadata.
- `files.log` records file analysis events observed by Zeek.
- `dns.log` records DNS activity.
- `zeek-cut` extracts selected fields from Zeek log records.
- The presence of a field or log file depends on the traffic observed and the policies loaded by Zeek.
- Filtering normal-looking DNS domains is only a triage step; legitimate services may also be used for command-and-control.

## References

- [Zeek - Log Files](https://docs.zeek.org/en/current/reference/zeekscript/log-files.html)
- [Corelight - Zeek Cheatsheets](https://github.com/corelight/zeek-cheatsheets)
- [Zeek - Documentation](https://docs.zeek.org/)

## Navigation

- [Class 07](../README.md)
- [Previous Activity - 7.3](../atividade-7.3-fontes-inteligencia/README.md)
- [Next Activity - 7.5](../atividade-7.5-analise-trafego-rita/README.md)
