# Activity 6.3 - Threat Hunting with Zeek

## Overview

This activity uses Zeek connection logs to investigate network communication patterns in Splunk. Search Processing Language (SPL) queries are used to identify destination ports, top communicating hosts, traffic volume, and traffic trends over time.

## Objectives

- Investigate Zeek connection records.
- Identify high destination ports.
- Identify the most active source and destination addresses.
- Analyze transferred data volumes.
- Visualize incoming and outgoing traffic over time.

## Data Source

| Item | Description |
|---|---|
| SIEM | Splunk Enterprise |
| Network Monitor | Zeek |
| Log File | `conn.log` |
| Source Host | `ip-192-168-98-10` |
| Main Fields | `id.orig_h`, `id.resp_h`, `id.resp_p`, `orig_bytes`, `resp_bytes`, `service` |

## Threat Hunting Queries

### 1. Identify Connections to Destination Ports Above 1024

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10" id.resp_p>1024 | chart count over service by id.resp_p
```

This query counts connections to destination ports above 1024 and organizes the results by service and destination port.

### 2. Identify the Top 10 Source IP Addresses

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10" | top id.orig_h | head 10
```

This query identifies source addresses with the highest number of recorded connections.

### 3. Analyze the Highest Outgoing Data Volumes

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10" | stats values(service) as Services sum(orig_bytes) as B by id.orig_h | sort -B | head 10 | eval MB=round(B/1024/1024,2) | eval GB=round(MB/1024,2) | rename id.orig_h as Source | fields Source B MB GB Services
```

This query aggregates outgoing bytes by source IP address, converts the totals into megabytes and gigabytes, and displays the ten highest results.

### 4. Identify the Top Destination IP Addresses

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10" | top id.resp_h | head 10
```

This query identifies destination addresses with the highest number of recorded connections.

### 5. Visualize Incoming and Outgoing Traffic Over Time

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10" | eval orig_megabytes=round(orig_bytes/1024/1024,2) | eval resp_megabytes=round(resp_bytes/1024/1024,2) | eval orig_gigabytes=round(orig_megabytes/1024,2) | eval resp_gigabytes=round(resp_megabytes/1024,2) | timechart sum(orig_gigabytes) AS "Outgoing Gigabytes",sum(resp_gigabytes) AS "Incoming Gigabytes" by service span=1h
```

This query converts traffic volume into gigabytes and creates a time-series visualization grouped by service.

## Expected Result

The queries provide different perspectives on Zeek connection data, supporting investigation of communication patterns and traffic volume.

The timechart query produces a line chart comparing incoming and outgoing traffic over time by service.

## Evidence

Step 6 - Line chart showing incoming and outgoing network traffic over time by service.

The required screenshot is included in the consolidated class-level evidence document:

- [View evidences.pdf](../evidences.pdf)

## Technical Notes

- `id.orig_h` represents the source address in the Zeek connection record.
- `id.resp_h` represents the destination address.
- `id.resp_p` represents the responder port.
- `orig_bytes` and `resp_bytes` represent byte counters in the original and response directions.
- Results depend on the network activity recorded in the lab environment.
- The queries use the original Zeek field names indexed by Splunk.

## References

- [Splunk - timechart command](https://help.splunk.com/en/splunk-enterprise/spl-search-reference/10.4/search-commands/timechart)
- [Zeek - Logging Framework](https://docs.zeek.org/en/current/frameworks/logging.html)

## Navigation

- [Class 06](../README.md)
- [Previous Activity - 6.2](../atividade-6.2-visualizando-logs-splunk/README.md)
- [Next Activity - 6.4](../atividade-6.4-preparando-elastic/README.md)


