 # Lab 03 — Analysis of Insight Nexus Breach

## Objective

Analyze a simulated multi-stage security incident using exported Wazuh logs and identify evidence related to credential compromise, persistence, data exfiltration, and unauthorized access.

## Investigation

The investigation was performed using the HTB-provided `wazuh_export.json` dataset.

The analysis focused on correlating Windows Security and Sysmon events with host information and identifying relevant indicators of compromise.

### Credential Compromise

Windows Security Event ID `4688` was analyzed to identify suspicious process creation and potential credential-dumping activity.

The investigation focused on:

* Process creation events
* Suspicious executables
* Parent-child process relationships
* User context

### Persistence

Persistence activity was identified through Windows service installation telemetry.

Windows Event ID `7045` was used to investigate newly installed services and identify suspicious service-related activity.

### Data Exfiltration

Sysmon Event ID `3` was used to investigate outbound network connections.

The analysis focused on:

* Destination IP addresses
* Destination ports
* Network protocols
* Executed processes
* Upload activity

### File Share Access

Windows network share events were reviewed to identify activity related to sensitive file shares and determine the associated user context.

## Commands Used

### Search for credential-dumping activity

```bash
grep -ni "mimikatz" wazuh_export.json
```

```bash
grep -ni -B 10 -A 10 "mimikatz" wazuh_export.json
```

### Search for persistence mechanisms

```bash
grep -ni "imagePath" wazuh_export.json
```

```bash
sed -n '7470,7550p' wazuh_export.json
```

### Search for exfiltration-related telemetry

```bash
grep -ni '"id": "90004"' wazuh_export.json
```

### Search for file share activity

```bash
grep -niE "fs01|projects" wazuh_export.json
```

## Key Takeaways

* Investigated a large Wazuh JSON dataset using command-line tools.
* Used Windows Event ID `4688` to investigate suspicious process creation.
* Used Event ID `7045` to investigate persistence through Windows services.
* Used Sysmon Event ID `3` to investigate outbound network activity.
* Investigated Windows file share activity.
* Used targeted `grep` and `sed` searches to reduce a large dataset into relevant investigative evidence.
* Correlated process, persistence, network, and file-sharing telemetry during incident analysis.

## Notes

No screenshots or question answers are included in this report.

The focus is on documenting the investigation methodology, relevant telemetry, and command-line techniques used during the lab.
