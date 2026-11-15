# Activity 5.3 — Analyzing an Enterprise-Scale Network Architecture

## Objective

Analyze an enterprise network architecture containing technologies and devices commonly found in corporate environments.

The diagram described in the course material includes mobility and VPN, physical and virtual network segmentation, a datacenter with mainframes, lightweight WLAN infrastructure, VoIP, and network traffic monitoring and analysis.

The activity requires identifying and explaining at least one strength and one weakness of the proposed architecture.

## Analysis

### Strength — Granular monitoring and defense in depth

The architecture includes mechanisms that improve network visibility and security monitoring, such as:

- Aggregation TAP infrastructure.
- Intrusion Detection Systems (IDS).
- Network Security Management capabilities.
- Traffic collection and analysis across different network segments.
- Perimeter firewalls.
- Internal datacenter firewalls.

An Aggregation TAP can provide access to network traffic for monitoring and analysis tools. This can help security teams observe communication across relevant network segments.

IDS and NSM technologies support the detection and investigation of suspicious traffic, while multiple firewall layers provide additional protection between network zones.

The combination of these mechanisms supports defense in depth and improves the ability to detect and investigate security incidents.

The architecture can also provide valuable telemetry from different technologies and segments, helping analysts identify suspicious communications, lateral movement, and other anomalous behavior.

### Weakness — Operational complexity and system interdependence

The architecture integrates multiple technologies, including:

- Mainframes.
- VPN connectivity.
- VoIP.
- MPLS.
- WLAN controllers.
- Physical and virtual network segments.
- Datacenter services.
- Central network switching and firewall capabilities.

The diversity of technologies increases the complexity of monitoring, troubleshooting, and correlating security events.

Different systems may produce logs in different formats, use different timestamps, and expose different levels of telemetry. Without centralized collection, normalization, and correlation, investigating events across the enterprise can become difficult.

Another concern is the dependency on the Core Switch with Firewall. If this component centralizes a significant portion of network communication, a failure or incorrect configuration can affect multiple segments and disrupt services required by the CSIRT.

Possible improvements include:

- Redundant core switching and firewall components.
- High-availability configurations.
- Separate management and monitoring networks.
- Centralized log collection and normalization.
- Consistent time synchronization across systems.
- Documented network dependencies.
- Continuous health monitoring of critical components.
- Tested failover and recovery procedures.

## Technical assessment

The architecture provides extensive monitoring opportunities and multiple security layers. These capabilities are important in enterprise environments where incidents may involve several network technologies and infrastructure components.

However, monitoring coverage alone is insufficient if events cannot be correlated effectively. A consistent logging strategy and resilient network design are necessary to make the architecture operationally effective.

## Conclusion

The main strength is the combination of granular network monitoring and defense in depth, supported by traffic analysis, IDS, NSM, and multiple firewall layers.

The main weakness is the operational complexity caused by integrating many different technologies and the potential dependency on a central Core Switch with Firewall. Redundancy and centralized event correlation are important improvements.

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)
