# Hackers do Bem - Specialization | Module 02 - Class 06

This class covers the collection, processing, and analysis of network data using SIEM platforms. The practical activities focus on forwarding Zeek logs to Splunk and Elastic, performing searches, building visualizations, and applying threat hunting queries.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Specialization - Incident Response and Digital Forensics |
| Module | 02 - Data Processing |
| Class | 06 |
| Main Topic | Data Collection, Processing, and Analysis using SIEM/SOAR |
| Main Technologies | Zeek, Splunk, Elastic Stack, Filebeat |

## Practical Activities

| Activity | Topic | Description | View |
|---|---|---|---|
| 6.1 | Preparing Splunk to Receive Zeek Logs | Create and configure a Splunk index to receive Zeek data. | [View Activity](./atividade-6.1-preparando-splunk-zeek/README.md) |
| 6.2 | Visualizing Zeek Logs in Splunk | Configure log forwarding and search for Zeek events in Splunk. | [View Activity](./atividade-6.2-visualizando-logs-splunk/README.md) |
| 6.3 | Threat Hunting with Zeek | Use SPL queries to investigate network connections, traffic volume, and communication patterns. | [View Activity](./atividade-6.3-threat-hunting-zeek-splunk/README.md) |
| 6.4 | Preparing Elastic to Receive Zeek Logs | Start and verify the Elasticsearch, Kibana, and Logstash services. | [View Activity](./atividade-6.4-preparando-elastic/README.md) |
| 6.5 | Sending Zeek Data to Elastic | Configure Filebeat integration and analyze Zeek events using Kibana and KQL. | [View Activity](./atividade-6.5-enviando-zeek-elastic/README.md) |

## Environment

The practical activities use the `forenseLinux` virtual machine provided by the training environment.

| Component | Description |
|---|---|
| Zeek | Network security monitoring and log generation |
| Splunk Enterprise | Log indexing, search, and visualization |
| Splunk Universal Forwarder | Collection and forwarding of Zeek logs |
| Elasticsearch | Storage and search engine for network events |
| Logstash | Data processing pipeline |
| Kibana | Data exploration and visualization |
| Filebeat | Collection and forwarding of Zeek logs to Elastic |

## Tools and Technologies

- Zeek
- Splunk Enterprise
- Splunk Universal Forwarder
- Elasticsearch
- Logstash
- Kibana
- Filebeat
- SPL (Search Processing Language)
- KQL (Kibana Query Language)
- Linux

## Learning Outcomes

- Configure Zeek to generate JSON-formatted logs.
- Prepare Splunk to receive and index network monitoring data.
- Configure log forwarding using Splunk Universal Forwarder.
- Search and analyze Zeek connection logs using SPL.
- Create time-based visualizations to investigate network traffic.
- Verify Elastic Stack services and their availability.
- Forward Zeek logs to Elastic using Filebeat.
- Use KQL to filter network events and investigate suspicious activity.

## Evidence Requirements

A single PDF document must contain the screenshots required for all five practical activities:

| Activity | Required Evidence |
|---|---|
| 6.1 | Step 4 - Splunk index creation page showing the `zeek` index name. |
| 6.2 | Step 8 - Splunk search results displaying data collected from the Zeek log directory. |
| 6.3 | Step 6 - Line chart showing incoming and outgoing network traffic over time by service. |
| 6.4 | Step 9 - Terminal output confirming that Elasticsearch, Kibana, and Logstash are running. |
| 6.5 | Step 5 - Kibana confirmation showing that Zeek data was successfully received. |

The screenshots must be legible and demonstrate the completion of the required steps.

## Technical Notes

- Zeek logs must be generated in JSON format for the described Splunk and Elastic workflows.
- Splunk Universal Forwarder and Splunk Enterprise use different installation paths and executables.
- The Universal Forwarder's `inputs.conf` defines monitored data sources, while `outputs.conf` defines forwarding destinations.
- The Filebeat Zeek module processes Zeek log data and provides predefined visualizations.
- KQL is used to filter events in Kibana. Aggregations and visualizations are configured separately through Kibana.
- Credentials used in the training environment are intentionally omitted from this documentation.

## References

- [Splunk - Configure the Universal Forwarder using configuration files](https://help.splunk.com/en/splunk-cloud-platform/forward-and-process-data/universal-forwarder-manual/9.1/configure-the-universal-forwarder/configure-the-universal-forwarder-using-configuration-files)
- [Splunk - Configure forwarding with outputs.conf](https://help.splunk.com/en/data-management/forward-data/universal-forwarder-manual/9.1/forward-data/configure-forwarding-with-outputs.conf)
- [Splunk - timechart command](https://help.splunk.com/en/splunk-enterprise/spl-search-reference/10.4/search-commands/timechart)
- [Elastic - Filebeat Zeek module](https://www.elastic.co/docs/reference/beats/filebeat/filebeat-module-zeek)
- [Elastic - Zeek Integration](https://www.elastic.co/docs/reference/integrations/zeek)
- [Elastic - Kibana Query Language](https://www.elastic.co/docs/reference/query-languages/kql)
- [Elastic - The Elastic Stack](https://www.elastic.co/docs/products/elastic-stack)

## Navigation

- [Module 02](../README.md)
- [Next Class](../aula-07/README.md)
