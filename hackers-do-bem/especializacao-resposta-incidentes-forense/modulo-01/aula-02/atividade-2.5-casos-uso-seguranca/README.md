# Activity 2.5 — Security Monitoring Use Cases with Splunk

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Platform:** Splunk Enterprise 9.0.3
> **Status:** Completed

## 1. Objective

Explore security monitoring use cases by searching Linux authentication logs for privileged activity and events relevant to incident investigations.

The activity uses Splunk Search Processing Language (SPL) to filter events and select relevant fields.

## 2. Monitoring Scenarios

The activity report describes the following monitoring scenarios:

| Scenario | Investigation Objective |
|---|---|
| Root activity | Identify commands executed with root privileges |
| Suspicious processes | Investigate unusual process-related activity |
| Critical file changes | Monitor changes to sensitive files |
| Network connections | Investigate network-related events |
| Privilege escalation | Identify privileged operations and account activity |

The exact additional queries and outputs for every scenario were not preserved in the available transcription.

The following section documents the exact search that was recorded.

## 3. Recorded SPL Query

The screenshot transcription contains:

```spl
index=* sourcetype="linux_secure" source="/var/log/auth.log" "COMMAND=" "USER=root"
| table _time, host, cmd
```

The query was executed in the Search & Reporting interface.

## 4. Search Breakdown

### Index Selection

```spl
index=*
```

Searches across available indexes.

### Sourcetype Filtering

```spl
sourcetype="linux_secure"
```

Limits results to events associated with the specified Linux security sourcetype.

### Source Filtering

```spl
source="/var/log/auth.log"
```

Restricts the events to the Linux authentication log.

### Keyword Filtering

```spl
"COMMAND=" "USER=root"
```

Filters for events containing both terms.

This search is intended to locate command-related activity associated with the root user.

### Field Selection

```spl
| table _time, host, cmd
```

The `table` command transforms the output into a table containing the specified fields.

| Field | Purpose |
|---|---|
| `_time` | Event timestamp |
| `host` | Host associated with the event |
| `cmd` | Command value extracted from the event |

The field extraction and availability depend on the indexed data and its configuration.

## 5. Search Time Range

The screenshot records the selected interval as:

```text
Last 24 hours
```

The interface reported:

```text
17 events
```

The recorded range was:

```text
May 7, 2026 9:00:00 PM
to
May 8, 2026 9:09:11 PM
```

## 6. Observed Results

The activity transcription preserves five sample rows with the host and timestamp fields.

| Row | Host | Time |
|---|---|---|
| 1 | ip-192-168-98-10 | 2026-05-08 20:51:56.353 |
| 2 | ip-192-168-98-10 | 2026-05-08 20:52:09.098 |
| 3 | ip-192-168-98-10 | 2026-05-08 21:03:47.954 |
| 4 | ip-192-168-98-10 | 2026-05-08 20:03:23.265 |
| 5 | ip-192-168-98-10 | 2026-05-08 19:47:11.769 |

The complete command values were not preserved in the transcription, so they are not reconstructed here.

The screenshot also records:

```text
Statistics (17)
Patterns
Events
```

## 7. Technical Interpretation

The SPL expression combines index selection, source filtering, sourcetype filtering, and keyword matching.

The pipeline then uses the `table` command to display the event timestamp, host, and command fields.

This approach can support an investigation into privileged activity by allowing analysts to identify root-related command records.

The event count of 17 indicates that the recorded search returned 17 matching events during the selected time range.

The result count alone does not establish that every event represents malicious behavior.

## 8. Security Investigation Considerations

Root-related command execution is important to monitor because privileged operations can affect:

- User accounts.
- System configuration.
- Security settings.
- Access permissions.
- Installed software.
- Critical system resources.

Additional investigation should consider the execution context, the administrator responsible, the command's purpose, and whether the activity was authorized.

For a more complete use-case implementation, separate searches can be developed for process execution, file modifications, network connections, and privilege escalation.

Those additional SPL expressions are not represented as executed in this activity because their original queries were not preserved.

## 9. Results

The activity report records that the SPL search returned 17 events over the Last 24 hours interval.

The search results were presented through the Statistics tab and organized into the fields:

- `_time`
- `host`
- `cmd`

The activity demonstrates how Splunk can filter Linux authentication events and organize information relevant to security investigations.

## 10. Concepts Practiced

- Splunk Search Processing Language
- Index and sourcetype filtering
- Source selection
- Keyword searches
- Field selection
- Root activity investigation
- Privileged command monitoring
- Event counts
- Security monitoring use cases

## 11. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The evidence document includes the search expression, selected time range, and recorded result count.

## References

- [Splunk Search Command](https://help.splunk.com/en/splunk-enterprise/search/spl-search-reference/9.2/search-commands/search)
- [Splunk Table Command](https://help.splunk.com/en/splunk-enterprise/search/spl-search-reference/10.6/search-commands/table)
- [Splunk SPL Syntax](https://help.splunk.com/en/splunk-enterprise/search/spl-search-reference/9.0/introduction/understanding-spl-syntax)

---

[Back to Class 02](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
