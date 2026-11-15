# Activity 3.3 — Understanding Zeek Logs and JSON

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Inspect Zeek log files and configure the platform to generate structured JSON output.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Log Directory | /opt/zeek/logs/current |
| Main Log | conn.log |
| Output Format | JSON |

## Procedure

### 1. Inspect Connection Logs

Access the current log directory:

```bash
sudo su
cd /opt/zeek/logs/current
nano conn.log
```

The connection log provides information about network connections observed by Zeek.

### 2. Stop Zeek

Stop the service before applying the logging configuration:

```bash
sudo /opt/zeek/bin/zeekctl stop
```

### 3. Enable JSON Output

Edit the site configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add:

```zeek
# Output to JSON
@load policy/tuning/json-logs.zeek
```

### 4. Restart Zeek

Start the service:

```bash
sudo /opt/zeek/bin/zeekctl start
```

### 5. Verify Generated Logs

Inspect the current log directory:

```bash
cd /opt/zeek/logs/current
ls -l
```

Alternatively, inspect the connection log:

```bash
nano conn.log
```

The activity report records that the generated log files were inspected in the current log directory.

## Understanding File Analysis Records

The training material demonstrates JSON records containing fields such as:

- `fuid`: Unique file identifier.
- `tx_hosts`: Hosts that transferred the file.
- `rx_hosts`: Hosts that received the file.
- `conn_uids`: Connection identifiers associated with the file.
- `source`: Source protocol, such as HTTP.
- `analyzers`: File analyzers applied.
- `mime_type`: Detected MIME type.
- `seen_bytes` and `total_bytes`: Observed and expected file sizes.
- `md5`, `sha1`, and `sha256`: File hashes.

These fields help correlate file activity with network connections and support forensic investigation.

## Result

The activity report records that the Zeek log directory was inspected after enabling JSON output.

The exercise demonstrates how structured logging makes network and file analysis data easier to process and correlate.

## Concepts Practiced

- Zeek connection logs
- JSON log configuration
- Structured security event data
- File metadata analysis
- Log inspection
- Event correlation

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
