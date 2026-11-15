# Activity 6.2 - Visualizing Zeek Logs in Splunk

## Overview

This activity configures log collection and forwarding so that Zeek network monitoring events can be searched in Splunk Enterprise.

The Splunk Universal Forwarder collects the source data and forwards it to the configured receiving instance.

## Objectives

- Configure the Splunk Universal Forwarder.
- Apply the provided `inputs.conf` and `outputs.conf` files.
- Monitor the Zeek log directory.
- Search for forwarded Zeek events in Splunk.

## Environment

| Component | Description |
|---|---|
| Log Source | Zeek |
| Universal Forwarder | `/opt/splunkforwarder` |
| Configuration Directory | `/opt/splunkforwarder/etc/system/local` |
| Zeek Logs | `/opt/zeek/logs/current` |
| Splunk Enterprise | `/opt/splunk` |

## Procedure

### 1. Configure the Universal Forwarder

The configuration files are provided by the training environment in `/curso/aula6/`.

Stop the Universal Forwarder before applying the provided configurations:

```bash
sudo /opt/splunkforwarder/bin/splunk stop
```

Copy the configuration files into the local system configuration directory:

```bash
sudo cp /curso/aula6/inputs.conf /opt/splunkforwarder/etc/system/local/inputs.conf
sudo cp /curso/aula6/outputs.conf /opt/splunkforwarder/etc/system/local/outputs.conf
```

Enable startup at boot and start the Universal Forwarder:

```bash
sudo /opt/splunkforwarder/bin/splunk enable boot-start
sudo /opt/splunkforwarder/bin/splunk start
```

### 2. Inspect Forwarder Logs

```bash
less /opt/splunkforwarder/var/log/splunk/splunkd.log
```

Check for startup or forwarding errors.

### 3. Monitor Zeek Logs in Splunk

In Splunk Enterprise:

1. Open **Add Data**.
2. Select **Monitor**.
3. Choose **Files & Directories**.
4. Select `/opt/zeek/logs/current`.
5. Complete the configuration and submit the data source.

### 4. Search for Zeek Events

Search for events from the monitored directory:

```spl
source="/opt/zeek/logs/current/*" host="ip-192-168-98-10"
```

To focus on connection logs:

```spl
source="/opt/zeek/logs/current/conn.log" host="ip-192-168-98-10"
```

## Expected Result

Zeek log events are searchable in Splunk Enterprise, including data collected from the Zeek log directory.

## Evidence

The required screenshot is **Step 8**, showing Splunk search results for the Zeek log directory query.

## Technical Notes

- `inputs.conf` controls how the Universal Forwarder collects data.
- `outputs.conf` defines the forwarding destination.
- Configuration changes require the Universal Forwarder to be restarted.
- `/opt/splunkforwarder/bin/splunk` is the Universal Forwarder executable.
- `/opt/splunk/bin/splunk` is the Splunk Enterprise executable.
- Credentials from the training environment are intentionally omitted.

## References

- [Splunk - Configure the Universal Forwarder using configuration files](https://help.splunk.com/en/splunk-cloud-platform/forward-and-process-data/universal-forwarder-manual/9.1/configure-the-universal-forwarder/configure-the-universal-forwarder-using-configuration-files)
- [Splunk - Configure forwarding with outputs.conf](https://help.splunk.com/en/data-management/forward-data/universal-forwarder-manual/9.1/forward-data/configure-forwarding-with-outputs.conf)

## Navigation

- [Class 06](../README.md)
- [Previous Activity - 6.1](../atividade-6.1-preparando-splunk-zeek/README.md)
- [Next Activity - 6.3](../atividade-6.3-threat-hunting-zeek-splunk/README.md)
