# Activity 14.2 — Network Evidence Analysis with NetworkMiner

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 14  
> **Environment:** forenseWin VM  
> **Status:** Completed

## 1. Objective

Analyze a packet capture using NetworkMiner and examine image artifacts automatically reconstructed from the captured network traffic.

The activity uses:

```text
captura_rede.pcap
```

NetworkMiner processes the packet capture and organizes extracted network artifacts through its graphical interface.

The focus of this exercise is the **Images** tab, where the analyst can view thumbnails of recovered image files.

The objective is to demonstrate how a network forensic analysis tool can extract application-level artifacts from a PCAP without requiring the analyst to reconstruct every transferred file manually.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseWin` |
| Operating System | Windows |
| Network Forensic Tool | NetworkMiner |
| Input File | `captura_rede.pcap` |
| Input Format | PCAP |
| Main Interface Tab | Images |
| Analysis Type | Offline packet capture analysis |
| Evidence | Recovered image thumbnails |

The activity uses an existing packet capture supplied by the course.

## 3. NetworkMiner Concepts

### NetworkMiner

NetworkMiner is a network forensic analysis tool designed to extract and present information from network traffic.

It can analyze packet captures offline and identify artifacts such as:

- Hosts.
- Sessions.
- Hostnames.
- Open ports.
- Transferred files.
- Images.
- Certificates.
- Credentials.
- Other application-level information supported by the protocols being analyzed.

The tool presents its findings through a graphical interface organized into different tabs.

### Offline PCAP Analysis

A PCAP file contains captured network packets.

NetworkMiner can open an existing PCAP and analyze its contents without generating traffic on the network.

This allows an investigator to work with a previously acquired capture.

### Automatic File Reconstruction

NetworkMiner attempts to identify and reconstruct files transferred through supported protocols.

The recovered files are presented in the application interface.

When extracted files are images, they can be displayed in the Images tab.

This reduces the need to manually follow individual packet streams to locate every image artifact.

### Images Tab

The Images tab provides a visual overview of the image files extracted from the analyzed traffic.

The application displays image thumbnails, allowing the analyst to review the available visual evidence.

The thumbnails help identify potentially relevant images before performing a more detailed examination of individual files.

## 4. Procedure

### Step 1 — Open NetworkMiner

The Windows forensic workstation was accessed.

NetworkMiner was opened from the installed applications.

The tool provides a graphical interface for loading packet captures and presenting extracted network artifacts.

### Step 2 — Load the Packet Capture

The supplied file was opened in NetworkMiner:

```text
captura_rede.pcap
```

The PCAP file contains the network traffic used in the exercise.

NetworkMiner parses the capture and attempts to identify hosts, sessions, transferred content, and other supported artifacts.

### Step 3 — Allow Artifact Processing

After the packet capture is loaded, NetworkMiner processes the available packets.

The application may organize the extracted information into different tabs.

The extracted files are generated from the content present in the packet capture and depend on the protocols and data available in the evidence.

### Step 4 — Examine the Images Tab

The **Images** tab was selected.

The interface displayed thumbnail previews of image files recovered from the packet capture.

The visual result demonstrates that NetworkMiner identified and reconstructed image artifacts from the captured traffic.

The exact image names, image count, and individual file sizes are not included in the supplied activity summary.

They should be taken from the original application screenshot rather than reconstructed from the description.

## 5. Expected Results

The expected result is the presentation of recovered image thumbnails in NetworkMiner.

| Item | Result |
|---|---|
| Network Analysis Tool | NetworkMiner |
| Input Capture | `captura_rede.pcap` |
| Processing Mode | Offline PCAP analysis |
| Main Evidence Tab | Images |
| Expected Artifact | Reconstructed image files |
| Visual Result | Image thumbnails |

The exercise demonstrates automatic file extraction from network traffic.

## 6. Technical Analysis

### Network Artifacts and Application Data

A packet capture contains more than endpoint addresses and port numbers.

Depending on the protocol, it may also contain application data that can be reconstructed into files or messages.

NetworkMiner provides a host-oriented way of examining these artifacts.

The analyst can move from general host information to extracted files and other content.

### Why the Images Tab Is Useful

Image thumbnails make it easier to identify visual content recovered from the network.

This can be useful in investigations involving:

- Unauthorized file transfers.
- Suspicious downloads.
- Data exfiltration.
- Unusual image transfers.
- Web browsing activity.
- Communications involving transferred media.

The images must still be correlated with packet timestamps, endpoints, sessions, and other evidence.

### Reconstruction Limitations

Automatic extraction depends on the information present in the PCAP.

A file may not be recoverable when:

- The capture begins after the transfer has started.
- Required packets are missing.
- The application data is encrypted.
- The protocol is not supported by the tool.
- The transferred content is incomplete.

The absence of an image in the Images tab does not prove that no image was transferred.

### Evidence Validation

Recovered image files should be examined individually.

An analyst should verify whether the file opens and whether its contents correspond to the recovered data.

If the investigation requires stronger evidence integrity, the extracted files can be hashed and documented separately.

## 7. Results and Interpretation

The activity demonstrates how NetworkMiner can analyze an existing PCAP and automatically recover image files transmitted through supported protocols.

The Images tab provides a visual summary of the recovered artifacts.

The thumbnails allow the analyst to identify relevant images and proceed with further examination.

The recovered images should be correlated with the associated hosts, sessions, packet timestamps, and other available artifacts.

## 8. Concepts Practiced

- Network forensics
- PCAP analysis
- NetworkMiner
- Offline traffic analysis
- Host identification
- Session analysis
- Application-level artifact extraction
- File reconstruction
- Image recovery
- Image thumbnails
- Evidence correlation
- Network evidence validation

## 9. Evidence

**Required screenshot: Print 4 — PDF page 2.**

The screenshot should display NetworkMiner with the **Images** tab selected.

The recovered image thumbnails should be visible in the application interface.

The screenshot should make it possible to identify that the images were reconstructed from:

```text
captura_rede.pcap
```

[View Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 14.2 is on page 2 of the consolidated PDF.

## References

- [NetworkMiner — Official Website](https://www.netresec.com/?page=NetworkMiner)
- [NetworkMiner — Security Onion Documentation](https://docs.securityonion.net/en/3/main/networkminer/)
- [NetworkMiner Resources and Manuals](https://www.netresec.com/?page=Resources)
- [Forensics Wiki — NetworkMiner](https://forensics.wiki/networkminer/)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 14.3](../atividade-14.3-networkminer-smtp/README.md)
