# Activity 7.5 - Network Traffic Analysis with RITA

## Overview

This activity uses RITA (Real Intelligence Threat Analytics) to analyze Zeek logs and identify suspicious network communication patterns. The practical exercise imports IcedID-related PCAP data into a RITA dataset and investigates potential beaconing activity.

## Objectives

- Prepare the RITA environment.
- Generate Zeek logs from PCAP files.
- Import Zeek logs into a RITA dataset.
- Analyze possible beaconing and command-and-control communication.
- Export RITA results to a CSV file for inspection.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Network Monitor | Zeek |
| Traffic Analysis | RITA |
| Database Component | MongoDB |
| Working Directory | `/opt/rita` |
| Dataset | `icedid` |

## Procedure

### 1. Install and Verify RITA

The training environment provides the RITA 5.0.6 installer:

```bash
sudo /opt/rita-v5.0.6-installer/install_rita.sh 127.0.0.1
```

Verify the RITA installation and configuration:

```bash
sudo rita -version
sudo rita test-config
```

The installation and dependency steps are specific to the supplied training VM.

### 2. Generate Zeek Logs from the IcedID PCAP

Move to the RITA working directory:

```bash
cd /opt/rita
```

Process the first PCAP:

```bash
sudo /opt/zeek/bin/zeek -Cr /opt/rita/2023-01-18-part-1-IcedID-traffic-carved-and-santized.pcap
```

Import the generated Zeek logs into the `icedid` dataset:

```bash
sudo rita import --database=icedid --logs=/opt/rita/ --rolling
```

The `--rolling` option is included because it is part of the course's practical procedure.

### 3. Add the Second PCAP to the Dataset

The course exercise processes a second capture and adds its Zeek logs to the same dataset.

Remove only the generated `.log` files from the lab working directory after confirming that the first import has completed:

```bash
sudo rm /opt/rita/*.log
```

Process the second PCAP:

```bash
sudo /opt/zeek/bin/zeek -Cr /opt/rita/2023-01-18-part-2-IcedID-C2-then-Cobalt-Strike-carved-and-sanitized.pcap
```

Import the additional logs:

```bash
sudo rita import --database=icedid --logs=/opt/rita/ --rolling
```

### 4. Review the RITA Dataset

Open the dataset in the RITA terminal interface:

```bash
sudo rita view icedid
```

The course example identifies communication from `10.1.18.101` to `jumptoupd.com` as suspicious beaconing activity.

The sample material reports 35 connections from that host to the destination domain. Actual output depends on the supplied PCAP files and the imported dataset.

### 5. Export Results to CSV

Export the dataset to a file:

```bash
sudo su
rita view --stdout icedid > /opt/rita/icedid_csv
exit
```

Open the generated file:

```bash
sudo nano /opt/rita/icedid_csv
```

## Expected Result

RITA imports Zeek-generated network metadata into the `icedid` dataset and presents connection patterns that can be investigated for beaconing and possible command-and-control behavior.

The CSV output makes the analysis results available for direct inspection in a text editor.

## Evidence

**Required screenshot: Step 6 - Print 10, PDF page 5.**

The screenshot must show the `icedid_csv` file in the terminal editor, highlighting the suspicious persistent connections from `10.1.18.101` to the C2 domain.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- RITA uses Zeek logs as input for network traffic analysis.
- RITA detects patterns such as beaconing, long connections, and DNS tunneling.
- The `--rolling` option is intended for datasets that accumulate recent network data. Current RITA guidance warns that importing older data with this option may produce incorrect results.
- The training exercise retains its supplied commands to reproduce the lab workflow; select the import mode according to data timestamps in other environments.
- The course uses a legacy RITA 5 installer path. Current RITA installation requirements include Docker Engine and the Compose plugin.
- PCAP analysis involving suspected malware should be performed only inside an isolated lab environment.

## References

- [RITA - Real Intelligence Threat Analytics](https://github.com/activecm/rita)
- [RITA - Importing and Searching Data](https://github.com/activecm/rita# importing)
- [Zeek - Log Files](https://docs.zeek.org/en/current/reference/zeekscript/log-files.html)

## Navigation

- [Class 07](../README.md)
- [Previous Activity - 7.4](../atividade-7.4-threat-hunting-zeek/README.md)
- [Module 02](../../README.md)
