# Activity 2.1 — Splunk Enterprise

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 02
> **Environment:** forenseLinux VM
> **Platform:** Splunk Enterprise 9.0.3
> **Status:** Completed

## 1. Objective

Start Splunk Enterprise, access the web interface, and prepare the platform for security log monitoring and incident investigation.

Splunk Enterprise is a platform used to collect, index, search, analyze, and visualize machine-generated data.

In this activity, it is used as the central interface for examining Linux authentication logs.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| SIEM | Splunk Enterprise |
| Version | 9.0.3 |
| Host | 192.168.98.10 |
| Web Interface | Port 8000 |
| Main Application | Search & Reporting |
| Log Source | /var/log/auth.log |

## 3. Procedure

### Step 1 — Start the Splunk Service

The original activity report records that the Splunk service was started in the forenseLinux VM.

The exact startup command was not preserved in the available transcription, so it is intentionally not reconstructed as a confirmed execution command.

The conventional command for an installation under `/opt/splunk` is:

```bash
sudo /opt/splunk/bin/splunk start
```

This is an additional reference command, not a verified command from the student's screenshot.

### Step 2 — Access Splunk Web

Open a browser and access:

```text
http://192.168.98.10:8000
```

Authenticate with the administrator account configured in the environment.

The password used in the exercise is intentionally not included in this public portfolio.

The interface displayed Splunk Enterprise 9.0.3.

### Step 3 — Open Search & Reporting

Navigate to the Search & Reporting application.

The available interface includes:

- Search
- Analytics
- Datasets
- Reports
- Alerts
- Dashboards

The activity prepares the environment for the subsequent log searches.

## 4. Initial Search Attempt

The available screenshot transcription records the following search:

```spl
source="/var/log/auth.log" host="ip-192-168-98-10" sourcetype="linux_secure"
```

The selected time range was:

```text
All time
```

The search was intended to retrieve events from the Linux authentication log.

## 5. Observed License Error

The initial search displayed the following error:

```text
Error in 'litsearch' command:
Your Splunk license expired or you have exceeded your license limit too many times.
Renew your Splunk license by visiting www.splunk.com/store
or calling 866.GET.SPLUNK.

The search job has failed due to an error.
You may be able view the job in the Job Inspector.
```

The interface showed:

```text
Events (0)
Patterns
Statistics
Visualization
```

This was an actual environment limitation recorded by the initial screenshot.

## 6. Technical Interpretation

The search expression contains three important field constraints:

| Field | Value | Meaning |
|---|---|---|
| `source` | /var/log/auth.log | Identifies the log source |
| `host` | ip-192-168-98-10 | Filters the originating host |
| `sourcetype` | linux_secure | Identifies the event type |

The search is designed to retrieve authentication-related events from the target Linux system.

The license error prevented that particular search job from completing at the time of the first screenshot.

Later activity records show that subsequent searches returned authentication events.

## 7. Results

The activity report records successful access to the Splunk Enterprise 9.0.3 web interface.

The initial authentication log search encountered a license-related error.

The error is documented as an environmental finding rather than a successful search result.

Subsequent activities demonstrate additional searches and event visualization.

## 8. Concepts Practiced

- SIEM platform initialization
- Splunk Enterprise
- Splunk Web
- Search & Reporting
- Data sources
- Host and sourcetype filtering
- Search time ranges
- Splunk licensing
- Job execution errors

## 9. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The corresponding screenshot documents access to Splunk Enterprise and the initial search environment.

## References

- [Splunk Enterprise Documentation](https://help.splunk.com/en/splunk-enterprise)
- [Monitor Files and Directories with inputs.conf](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.3/get-data-from-files-and-directories/monitor-files-and-directories-with-inputs.conf)

---

[Back to Class 02](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
