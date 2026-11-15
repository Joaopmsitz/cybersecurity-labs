# Hackers do Bem - Specialization | Module 02 - Class 06

Practical activities covering the collection, processing, and analysis of network security data using SIEM platforms. The exercises forward Zeek logs to Splunk and Elastic for searching, threat hunting, and visualization.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 02 - Data Processing |
| Class | 06 |
| Main Topic | Data Collection, Processing, and Analysis using SIEM/SOAR |
| Main Technologies | Zeek, Splunk, Elasticsearch, Logstash, Kibana, Filebeat |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 6.1 | Preparing Splunk to Receive Zeek Logs | Inspect Zeek JSON logs and create a dedicated Splunk index. | [View Activity](./atividade-6.1-preparando-splunk-zeek/README.md) |
| 6.2 | Visualizing Zeek Logs in Splunk | Configure log forwarding and search for collected Zeek events. | [View Activity](./atividade-6.2-visualizando-logs-splunk/README.md) |
| 6.3 | Threat Hunting with Zeek | Investigate network connections and traffic patterns using SPL. | [View Activity](./atividade-6.3-threat-hunting-zeek-splunk/README.md) |
| 6.4 | Preparing Elastic to Receive Zeek Logs | Start and validate Elasticsearch, Kibana, and Logstash services. | [View Activity](./atividade-6.4-preparando-elastic/README.md) |
| 6.5 | Sending Zeek Data to Elastic | Forward Zeek logs with Filebeat and investigate events in Kibana. | [View Activity](./atividade-6.5-enviando-zeek-elastic/README.md) |

## Environment

The activities use the `forenseLinux` virtual machine provided by the training environment.

| Component | Purpose |
|---|---|
| Zeek | Network security monitoring and log generation |
| Splunk Enterprise | Log indexing, search, and visualization |
| Splunk Universal Forwarder | Log collection and forwarding |
| Elasticsearch | Data storage and search |
| Logstash | Data processing |
| Kibana | Data exploration and visualization |
| Filebeat | Log collection and forwarding to Elastic |

## Tools and Technologies

- Zeek
- Splunk Enterprise
- Splunk Universal Forwarder
- Elasticsearch
- Logstash
- Kibana
- Filebeat
- Search Processing Language (SPL)
- Kibana Query Language (KQL)
- Linux

## Learning Outcomes

- Configure Zeek to generate JSON-formatted logs.
- Prepare Splunk to index network monitoring data.
- Configure log forwarding using Splunk Universal Forwarder.
- Search and investigate Zeek connection logs using SPL.
- Build time-based network traffic visualizations.
- Verify Elastic Stack service availability.
- Forward Zeek logs with Filebeat.
- Filter network events using KQL in Kibana.

## Evidence

| Activity | Evidence | Required Capture |
|---|---|---|
| 6.1 | [6.1.pdf](./6.1.pdf) | Step 4 - Splunk index creation page displaying the `zeek` index name. |
| 6.2 | Pending | Step 8 - Splunk search results for the Zeek log directory. |
| 6.3 | Pending | Step 6 - Line chart showing incoming and outgoing traffic over time by service. |
| 6.4 | Pending | Step 9 - Terminal output confirming Elasticsearch, Kibana, and Logstash status. |
| 6.5 | Pending | Step 5 - Kibana confirmation that Zeek data was successfully received. |

The `6.1.pdf` file contains the evidence currently available for this class. The remaining evidence will be added as the activities are completed.

## Technical Notes

- Zeek logs must use JSON formatting for the parsing workflows described in these activities.
- Splunk Enterprise and Splunk Universal Forwarder use separate installation paths and executables.
- The Filebeat Zeek module follows the traditional Beats workflow used in this training environment.
- KQL filters documents; Kibana visualizations handle data presentation and aggregation.
- Training credentials and sensitive environment information are excluded from this documentation.

## References

- [Splunk - Configure the Universal Forwarder](https://help.splunk.com/en/splunk-cloud-platform/forward-and-process-data/universal-forwarder-manual/9.1/configure-the-universal-forwarder/configure-the-universal-forwarder-using-configuration-files)
- [Splunk - Configure forwarding with outputs.conf](https://help.splunk.com/en/data-management/forward-data/universal-forwarder-manual/9.1/forward-data/configure-forwarding-with-outputs.conf)
- [Splunk - timechart command](https://help.splunk.com/en/splunk-enterprise/spl-search-reference/10.4/search-commands/timechart)
- [Elastic - Filebeat Zeek Module](https://www.elastic.co/docs/reference/beats/filebeat/filebeat-module-zeek)
- [Elastic - Zeek Integration](https://www.elastic.co/docs/reference/integrations/zeek)
- [Elastic - Kibana Query Language](https://www.elastic.co/docs/reference/query-languages/kql)
- [Elastic - The Elastic Stack](https://www.elastic.co/docs/products/elastic-stack)

## Navigation

- [Module 02](../README.md)
- [Specialization Overview](../../README.md)
