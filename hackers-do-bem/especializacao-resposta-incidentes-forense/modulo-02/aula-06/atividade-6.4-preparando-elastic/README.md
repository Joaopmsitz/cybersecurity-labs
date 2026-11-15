# Activity 6.4 - Preparing Elastic to Receive Zeek Logs

## Overview

This activity prepares the Elastic Stack environment to receive and analyze network monitoring data. Elasticsearch, Kibana, and Logstash services are started and validated before the Zeek integration workflow.

## Objectives

- Start the Elastic Stack services.
- Verify Elasticsearch availability.
- Check the status of Kibana and Logstash.
- Record the service status output.

## Environment

| Component | Purpose |
|---|---|
| Elasticsearch | Data storage and search engine |
| Kibana | Data exploration and visualization |
| Logstash | Data processing pipeline |
| Linux | Lab operating system |

## Procedure

### 1. Start the Services

Start Elasticsearch:

```bash
sudo systemctl start elasticsearch
```

Start Kibana and Logstash:

```bash
sudo systemctl start kibana
sudo systemctl start logstash
```

### 2. Verify Service Status

```bash
sudo systemctl status elasticsearch kibana logstash --no-pager
```

### 3. Test Elasticsearch

Query the local Elasticsearch API:

```bash
curl -X GET "localhost:9200"
```

A successful response returns cluster and node information in JSON format.

### 4. Save the Service Status Output

Save the status information to the file required by the activity:

```bash
sudo systemctl status elasticsearch kibana logstash --no-pager > /home/aluno/atv_pratica_6-4.txt
```

Display the saved output:

```bash
cat /home/aluno/atv_pratica_6-4.txt
```

## Expected Result

Elasticsearch, Kibana, and Logstash are running and their status information is available in the required text file.

Elasticsearch responds to the local API request.

## Evidence

Step 9 - Terminal output confirming Elasticsearch, Kibana, and Logstash status.

The required screenshot is included in the consolidated class-level evidence document:

- [View evidences.pdf](../evidences.pdf)

## Technical Notes

- Elasticsearch provides storage and search capabilities.
- Kibana provides the interface for searching and visualizing indexed data.
- Logstash provides data ingestion and processing capabilities.
- Service status alone does not prove that data is being ingested; data arrival must be checked separately.

## References

- [Elastic - The Elastic Stack](https://www.elastic.co/docs/products/elastic-stack)
- [Elastic - Getting Started with the Stack](https://www.elastic.co/docs/get-started/the-stack)

## Navigation

- [Class 06](../README.md)
- [Previous Activity - 6.3](../atividade-6.3-threat-hunting-zeek-splunk/README.md)
- [Next Activity - 6.5](../atividade-6.5-enviando-zeek-elastic/README.md)


