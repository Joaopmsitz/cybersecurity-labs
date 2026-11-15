# Activity 10.5 - Logical Network Evidence Collection with Wireshark

## Overview

This activity uses Wireshark to inspect a previously captured network trace and extract logical evidence from HTTP traffic.

The supplied `captura_rede.cap` file is opened in Wireshark, filtered for HTTP packets, and examined using the Export Objects feature.

## Objectives

- Open the supplied network capture.
- Filter HTTP traffic.
- Identify transferred HTTP objects.
- Export the reconstructed objects.
- Verify the extracted files in the destination directory.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forensewin` |
| Analysis Tool | Wireshark |
| Capture File | `C:\curso\aula10\captura_rede.cap` |
| Export Destination | `C:\Users\aluno\Documents` |
| Protocol | HTTP |

## Procedure

### 1. Open the Network Capture

Start Wireshark on the supplied Windows laboratory machine.

Open the capture file:

```text
C:\curso\aula10\captura_rede.cap
```

Inspect the packets and identify the network protocols present in the capture.

### 2. Filter HTTP Traffic

Enter the following display filter:

```wireshark
http
```

Review the HTTP requests and identify requests that include transferred objects such as images.

### 3. Export HTTP Objects

Open the Wireshark menu:

**File > Export Objects > HTTP**

The dialog displays HTTP objects reconstructed from the packet capture.

Review the listed objects and select **Save All**.

### 4. Select the Export Destination

Choose:

```text
C:\Users\aluno\Documents
```

Complete the export operation.

### 5. Verify Extracted Files

Open the Documents directory and inspect the files exported from the network capture.

## Expected Result

Wireshark identifies HTTP objects within the supplied PCAP file and exports the selected objects to the Documents directory.

The extracted files can be examined separately as logical network evidence.

## Evidence

**Required screenshot: Step 8 - Print 4, PDF page 4.**

The screenshot should show the Wireshark **Export Objects > HTTP** window with the objects identified in the capture.

It should also demonstrate the export result, with the extracted files available in the Documents directory.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Wireshark display filters control which packets appear in the packet list.
- The `http` filter displays packets recognized as HTTP.
- Export Objects reconstructs supported transferred objects from captured protocol streams.
- The exported content should be handled as evidence and preserved separately from the original PCAP.
- Files extracted from a packet capture may be malicious. Do not execute suspicious recovered files.
- Preserve the original capture and document the extraction context.

## References

- [Wireshark - User's Guide](https://www.wireshark.org/docs/wsug_html/)
- [Wireshark - Exporting Data](https://www.wireshark.org/docs/wsug_html_chunked/ChIOExportSection.html)
- [Wireshark - Display Filters](https://www.wireshark.org/docs/man-pages/wireshark-filter.html)

## Navigation

- [Class 10](../README.md)
- [Previous Activity - 10.4](../atividade-10.4-dump-rede-tcpdump/README.md)
- [Module 02](../../README.md)
