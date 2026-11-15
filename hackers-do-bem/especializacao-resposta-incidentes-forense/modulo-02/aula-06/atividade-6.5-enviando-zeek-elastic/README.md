# Activity 6.5 - Sending Zeek Data to Elastic

## Overview

This activity forwards Zeek JSON logs to the Elastic Stack using Filebeat. The Zeek integration is enabled in Kibana to parse and explore network monitoring data.

## Objectives

- Verify that Zeek is configured to generate JSON logs.
- Deploy the Zeek configuration.
- Start and validate Filebeat.
- Enable the Zeek Logs module in Kibana.
- Search Zeek events using Kibana Query Language (KQL).

## Environment

| Component | Description |
|---|---|
| Network Monitor | Zeek |
| Log Directory | `/opt/zeek/logs/current` |
| Zeek Configuration | `/opt/zeek/share/zeek/site/local.zeek` |
| Log Collector | Filebeat |
| Data Platform | Elasticsearch |
| Interface | Kibana |

## Procedure

### 1. Verify Zeek JSON Logging

Open the Zeek local configuration file:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Ensure the following policy is loaded:

```zeek
@load policy/tuning/json-logs.zeek
```

Deploy the updated Zeek configuration:

```bash
sudo zeekctl deploy
```

### 2. Start and Verify Filebeat

Restart Filebeat:

```bash
sudo systemctl restart filebeat
```

Check the service status:

```bash
sudo systemctl status filebeat --no-pager
```

### 3. Enable the Zeek Logs Module in Kibana

In Kibana:

1. Open **Add Integrations**.
2. Search for **Zeek Logs**.
3. Select the Zeek Logs module available through Beats.
4. Open the module status section.
5. Select **Check Data**.
6. Confirm that data has been successfully received.
7. Open the Zeek Overview dashboard.

## KQL Queries

### 1. Find Zeek Connection Events

```kql
event.module:zeek AND event.dataset:zeek.connection
```

### 2. Find Connections to Destination Ports Above 1024

```kql
event.module:zeek AND event.dataset:zeek.connection AND destination.port > 1024
```

### 3. Find DNS NXDOMAIN Responses

```kql
event.module:zeek AND event.dataset:zeek.dns AND dns.response_code:NXDOMAIN
```

### 4. Find Expired Certificates

```kql
event.module:zeek AND event.dataset:zeek.x509 AND file.x509.not_after < now
```

## Dashboard

Open the Kibana dashboard area:

```text
/app/dashboards
```

Locate the **Filebeat Zeek Overview** dashboard to explore the ingested network monitoring data.

## Expected Result

Filebeat forwards Zeek JSON logs to the Elastic Stack, and Kibana confirms successful data reception from the Zeek module.

The connection, DNS, and certificate queries can be used to filter the ingested events.

## Evidence

Step 5 - Kibana confirmation that Zeek data was successfully received.

The required screenshot is included in the consolidated class-level evidence document:

- [View evidences.pdf](../evidences.pdf)

## Technical Notes

- The Filebeat Zeek module expects Zeek JSON-formatted logs.
- The `json-logs.zeek` policy enables JSON output in the Zeek configuration used by this activity.
- KQL filters documents by field values and conditions; it does not perform aggregations or sorting.
- This training activity uses the traditional Filebeat module workflow. Newer Elastic Zeek integrations may use Elastic Agent and should not be confused with the steps in this lab.

## References

- [Elastic - Filebeat Zeek Module](https://www.elastic.co/docs/reference/beats/filebeat/filebeat-module-zeek)
- [Elastic - Zeek Integration](https://www.elastic.co/docs/reference/integrations/zeek)
- [Elastic - Kibana Query Language](https://www.elastic.co/docs/reference/query-languages/kql)
- [Elastic - Collecting and Analyzing Zeek Data](https://www.elastic.co/blog/collecting-and-analyzing-zeek-data-with-elastic-security)

## Navigation

- [Class 06](../README.md)
- [Previous Activity - 6.4](../atividade-6.4-preparando-elastic/README.md)
- [Module 02](../../README.md)

