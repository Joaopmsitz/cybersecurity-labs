# Activity 3.1 — Configuring Zeek

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Validate the Zeek configuration, deploy the network monitoring service, and verify that the platform is running successfully.

Zeek is a passive, open-source network traffic analyzer used as a Network Security Monitor (NSM). It inspects observed network communications and generates structured logs that support security monitoring, investigations, and troubleshooting.

Unlike a traditional inline firewall, Zeek primarily observes and analyzes traffic rather than blocking connections directly.

The original project was initially developed under the name Bro in the 1990s by Vern Paxson.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Virtual Machine Address | 192.168.98.10 |
| Tool | Zeek |
| Installation Directory | /opt/zeek |
| Control Utility | zeekctl |
| Configuration Directory | /opt/zeek/share/zeek/site |
| Log Directory | /opt/zeek/logs/current/ |

## 3. Procedure

### Step 1 — Validate the Configuration

Open the terminal and execute:

```bash
sudo /opt/zeek/bin/zeekctl check
```

The `check` command verifies the Zeek configuration before deployment.

This validation helps identify configuration errors that could prevent the service from starting correctly.

### Step 2 — Deploy Zeek

Apply the configuration:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

The `deploy` command applies the current configuration and manages the startup of the Zeek processes.

### Step 3 — Verify Service Status

Execute:

```bash
sudo /opt/zeek/bin/zeekctl status
```

The expected service status in the assignment is:

```text
Running
```

The activity report records that the service status was successfully verified.

## 4. Troubleshooting

If Zeek does not start correctly, diagnostic information can be collected with:

```bash
sudo /opt/zeek/bin/zeekctl diag
```

This command helps investigate startup and runtime problems.

### Inspect the Current Log Directory

Open a root shell:

```bash
sudo su
```

List the files:

```bash
ls -l /opt/zeek/logs/current/
```

Leave the root shell:

```bash
exit
```

### Inspect Connection Logs

A connection log can be inspected with:

```bash
sudo su
tail /opt/zeek/logs/current/conn.log
exit
```

`conn.log` contains records of network connections observed by Zeek.

The log can be used to identify communication endpoints, ports, transport protocols, and connection identifiers.

## 5. Terminal Prompt Configuration for Evidence

The original activity requires the terminal prompt to display the student's alias together with the date and current time.

Example command provided in the assignment:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\u/meunome/g')"
```

Replace `meunome` with the alias used for the activity.

The command must be executed again whenever a new terminal session is opened.

## 6. Results

The activity report records that the `zeekctl status` command confirmed that the Zeek service was running.

Expected result:

```text
Running
```

The configuration and deployment procedures establish the base environment needed by the subsequent activities.

The assignment also identifies `/opt/zeek/logs/current/` as the location for current Zeek log files.

No additional command output beyond the recorded service status is represented as an observed result.

## 7. Technical Interpretation

The ZeekControl utility provides administrative operations for the monitoring installation.

| Command | Function |
|---|---|
| zeekctl check | Validates the configuration |
| zeekctl deploy | Applies the configuration and deploys processes |
| zeekctl status | Displays the status of managed processes |
| zeekctl diag | Collects diagnostic information |
| zeekctl stop | Stops the managed service |
| zeekctl start | Starts the managed service |

A successful status verification is an important prerequisite before enabling additional file analysis and extraction features.

## 8. Concepts Practiced

- Network Security Monitoring (NSM)
- Zeek architecture
- Configuration validation
- Service deployment
- Runtime status verification
- Linux terminal administration
- Network connection logging
- Initial troubleshooting

## 9. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot corresponds to Step 2 of the activity and documents the result of the `zeekctl status` command.

## References

- [Zeek Documentation](https://docs.zeek.org/en/master/)
- [Zeek Quick Start](https://docs.zeek.org/en/current/quickstart.html)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
