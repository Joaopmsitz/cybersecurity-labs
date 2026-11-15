# Activity 3.3 — Understanding Zeek Logs and JSON Output

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Inspect Zeek connection and file logs, understand their fields, and configure structured JSON output for easier event analysis and correlation.

The activity uses the current Zeek log directory:

```text
/opt/zeek/logs/current/
```

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Log Directory | /opt/zeek/logs/current/ |
| Initial Log | conn.log |
| Output Format | JSON |
| Main Configuration | /opt/zeek/share/zeek/site/local.zeek |

## 3. Procedure

### Step 1 — Inspect conn.log

Open a root shell:

```bash
sudo su
```

Navigate to the current log directory:

```bash
cd /opt/zeek/logs/current
```

Open the connection log:

```bash
nano conn.log
```

Exit Nano with `Ctrl + X`, then leave the root shell:

```bash
exit
```

The `conn.log` file records connection-related information observed by Zeek.

Depending on the traffic and the active configuration, the records can include:

- Connection timestamps.
- Unique connection identifiers.
- Origin and destination IP addresses.
- Origin and destination ports.
- Transport protocol.
- Application service.
- Connection duration.
- Number of transferred bytes.
- Connection state.

### Step 2 — Stop Zeek

Before changing the logging configuration, stop the service:

```bash
sudo /opt/zeek/bin/zeekctl stop
```

### Step 3 — Enable JSON Logging

Edit the main site configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add the following directive after the last existing line:

```zeek
# Output to JSON
@load policy/tuning/json-logs.zeek
```

The assignment uses the `.zeek` filename extension.

Save and exit Nano:

- `Ctrl + O`
- `Enter`
- `Ctrl + X`

### Step 4 — Start Zeek Again

Open a root shell:

```bash
sudo su
```

Start Zeek:

```bash
/opt/zeek/bin/zeekctl start
```

### Step 5 — Verify Generated Log Files

Navigate to the current log directory:

```bash
cd /opt/zeek/logs/current
```

List its contents:

```bash
ls -l
```

Alternatively, inspect the connection log:

```bash
nano conn.log
```

The assignment allows either the directory listing or the JSON-formatted log content as evidence.

If records are not immediately available, wait for network activity to be observed by Zeek.

## 4. Example JSON File Record from the Training Material

The assignment provides the following example of a file analysis record:

```json
{
  "ts": 1597593633.224633,
  "fuid": "FB4Sx62yaleypxnhIb",
  "tx_hosts": [
    "23.246.2.148"
  ],
  "rx_hosts": [
    "10.2.2.23"
  ],
  "conn_uids": [
    "CUgYfkjoZLP4BR8Ol"
  ],
  "source": "HTTP",
  "depth": 0,
  "analyzers": [
    "JPEG",
    "SHA1",
    "MD5",
    "SHA256"
  ],
  "mime_type": "image/jpeg",
  "duration": 0.01756000518798828,
  "local_orig": false,
  "is_orig": false,
  "seen_bytes": 58175,
  "total_bytes": 58175,
  "missing_bytes": 0,
  "overflow_bytes": 0,
  "timedout": false,
  "md5": "0671e92b0fb8ffe5724579c229a43689",
  "sha1": "e855561e88f0bc57733eafa05a9d7681d276e55a",
  "sha256": "fc58cf109988af3b3dbc499001ff300584eff638cb120405558d3df69c22fdf4"
}
```

**Important:** this JSON record is an illustrative example from the training material, not a claim that the exact record was generated during the student's execution.

## 5. Field Interpretation

| Field | Description |
|---|---|
| `ts` | Timestamp associated with the file event |
| `fuid` | Unique file identifier |
| `tx_hosts` | Hosts that transmitted the file |
| `rx_hosts` | Hosts that received the file |
| `conn_uids` | Connection identifiers associated with the file |
| `source` | Protocol or source from which the file was observed |
| `depth` | File analysis depth |
| `analyzers` | File analyzers applied to the sample |
| `mime_type` | MIME type identified by Zeek |
| `duration` | Observed file transfer duration |
| `local_orig` | Whether the originator was classified as local |
| `is_orig` | Whether the file source corresponds to the connection originator |
| `seen_bytes` | Number of bytes observed |
| `total_bytes` | Total file size recorded |
| `missing_bytes` | Bytes missing from the observed file data |
| `overflow_bytes` | Bytes not processed due to overlap or reassembly conditions |
| `timedout` | Indicates whether the file analysis timed out |
| `md5` | MD5 digest |
| `sha1` | SHA1 digest |
| `sha256` | SHA256 digest |

## 6. Technical Interpretation

JSON logging provides a structured representation in which field names are explicitly associated with their values.

For example:

```json
{
  "fuid": "FB4Sx62yaleypxnhIb",
  "mime_type": "image/jpeg",
  "total_bytes": 58175,
  "missing_bytes": 0
}
```

This makes the record easier to read and process programmatically.

The combination of `fuid` and `conn_uids` also enables correlation between file analysis and network connection logs.

The presence of all expected bytes, with `missing_bytes` equal to zero, indicates that the example file record contains the complete observed file content.

## 7. Results

The activity report records that JSON logging was enabled and that the generated files were inspected in:

```text
/opt/zeek/logs/current/
```

The report identifies the directory listing as the selected evidence option.

The example JSON above illustrates the expected structured file record and the metadata generated by the File Analysis Framework.

## 8. Important Technical Note

The assignment presents the loading directive as:

```zeek
@load policy/tuning/json-logs.zeek
```

Current official Zeek documentation also demonstrates the equivalent script loading using:

```zeek
@load policy/tuning/json-logs
```

Use the form compatible with the installed Zeek script path and the training environment.

JSON logs are useful for integration and programmatic analysis, although their field names add storage overhead compared with tab-separated logs.

## 9. Concepts Practiced

- Zeek connection logs
- File analysis logs
- JSON log configuration
- Structured security event data
- File identifiers and connection identifiers
- Cryptographic hashes
- Event correlation
- Missing and observed file bytes
- Log inspection and interpretation

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

Required screenshot: Step 5, showing the generated files in `/opt/zeek/logs/current/` or a JSON-formatted connection log.

## References

- [Zeek Logs](https://docs.zeek.org/en/current/tutorial/logs.html)
- [Zeek files.log Reference](https://docs.zeek.org/en/current/reference/logs/files.html)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
