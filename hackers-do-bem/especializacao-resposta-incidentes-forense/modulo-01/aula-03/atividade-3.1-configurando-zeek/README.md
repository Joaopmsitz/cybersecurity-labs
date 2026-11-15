# Activity 3.1 — Configuring Zeek

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Verify the Zeek configuration, deploy the service, and confirm that the network security monitoring platform is running correctly.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Control Utility | zeekctl |
| Installation Path | /opt/zeek |

## Procedure

### 1. Validate the Configuration

Execute:

```bash
sudo /opt/zeek/bin/zeekctl check
```

This command checks the Zeek configuration and verifies whether the installation is ready for deployment.

### 2. Deploy Zeek

Apply the configuration:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

### 3. Check Service Status

Execute:

```bash
sudo /opt/zeek/bin/zeekctl status
```

The expected status is:

```text
Running
```

## Troubleshooting

If Zeek does not initialize correctly, inspect its diagnostics:

```bash
sudo /opt/zeek/bin/zeekctl diag
```

Current log files can be listed with:

```bash
sudo ls -l /opt/zeek/logs/current/
```

Connection events can be inspected using:

```bash
sudo tail /opt/zeek/logs/current/conn.log
```

## Result

The activity report records that the Zeek status was verified successfully and that the service was running.

## Concepts Practiced

- Zeek configuration validation
- Service deployment
- Network security monitoring initialization
- Service status verification
- Basic troubleshooting
- Zeek log directory inspection

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
