# Activity 14.1 — Network Evidence Extraction with TCPFlow and Foremost

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 14  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Extract image files recovered from network-related evidence using TCPFlow and Foremost.

The activity demonstrates two complementary forensic techniques:

- TCP stream reconstruction with TCPFlow.
- File carving with Foremost.

TCPFlow reconstructs TCP conversations and stores the data transmitted through individual flows. Foremost searches an input file or image for recognizable file structures, allowing supported file types to be recovered even when the original filesystem structure is unavailable.

The confirmed extraction command is:

```bash
foremost -i imagem.dump -o extracao
```

The output is examined in:

```text
extracao/jpg
```

The recorded result contains five recovered JPEG images.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux |
| Forensic Task | Network evidence extraction |
| Network Reconstruction Tool | TCPFlow |
| File Carving Tool | Foremost |
| Input Artifact for Foremost | `imagem.dump` |
| Output Directory | `extracao` |
| JPEG Output Directory | `extracao/jpg` |
| Confirmed Recovered Files | 5 JPEG images |
| Evidence Terminal | Linux terminal with personalized prompt |

The exact source capture filename and the full TCPFlow command are not preserved in the supplied activity summary.

The confirmed Foremost input and output paths are documented without assuming how `imagem.dump` was generated.

## 3. Technical Concepts

### TCP Stream Reconstruction

TCPFlow is a command-line forensic utility that reconstructs data transmitted through TCP connections.

Unlike a packet-by-packet display, TCPFlow organizes the reconstructed data into separate files representing individual TCP flows.

This is useful when the investigator needs to examine the application data exchanged between network endpoints.

TCPFlow can help expose transferred content that is not immediately apparent from the packet headers alone.

A typical offline analysis syntax is:

```bash
tcpflow -r <capture.pcap> -o <flow_directory>
```

| Parameter | Function |
|---|---|
| `tcpflow` | Starts the TCPFlow utility |
| `-r` | Reads packets from an existing capture file |
| `<capture.pcap>` | Input packet capture |
| `-o` | Specifies the output directory |
| `<flow_directory>` | Directory used for reconstructed flows |

This is the general command syntax. The exact TCPFlow command and filenames used in the course procedure were not included in the supplied activity summary.

### File Carving

File carving is a forensic technique used to identify and recover files from raw data based on recognizable file structures.

It can be useful when directory entries or filesystem metadata are unavailable.

Foremost is a command-line file-carving utility that identifies file types using configured headers, footers, and internal structures.

It can recover supported formats from disk images and other input files.

### Foremost

The main command used in this activity is:

```bash
foremost -i imagem.dump -o extracao
```

| Parameter | Function |
|---|---|
| `foremost` | Starts the file-carving utility |
| `-i imagem.dump` | Defines the input file |
| `-o extracao` | Defines the directory where recovered files are written |

The command does not explicitly restrict extraction to JPEG files with `-t jpg`.

Foremost therefore uses the configured file types available to the installed version and configuration.

The activity then inspects the JPEG output directory specifically.

### JPEG Recovery

JPEG files commonly use recognizable signatures that allow forensic tools to identify candidate image data.

The recovered files are written to a directory organized by file type.

For this activity, the relevant output directory is:

```text
extracao/jpg
```

The presence of five images in this directory is the recorded result.

## 4. Procedure

### Step 1 — Prepare the Network Evidence

The activity uses network-related evidence for reconstruction and file extraction.

TCPFlow is used to reconstruct TCP streams from network traffic.

The general offline syntax is:

```bash
tcpflow -r <capture.pcap> -o <flow_directory>
```

The command reads an existing packet capture and stores reconstructed TCP flows in the selected output directory.

The source summary supplied for this documentation identifies TCPFlow as part of the activity but does not preserve the actual input filename, output directory, or full command used in the laboratory.

Those details should be transcribed from the original activity instructions if they need to be reproduced exactly.

### Step 2 — Identify the Data to Be Carved

The activity uses the file:

```text
imagem.dump
```

as input for Foremost.

The objective is to inspect the content of the supplied network-related data and recover recognizable image files.

The file is treated as forensic input evidence. The original should remain unchanged during the analysis.

### Step 3 — Execute Foremost

The extraction was performed with:

```bash
foremost -i imagem.dump -o extracao
```

The command instructs Foremost to examine `imagem.dump` and write recovered files under:

```text
extracao
```

Foremost creates output organized by file type.

The JPEG output is stored in:

```text
extracao/jpg
```

### Step 4 — Inspect the Recovered JPEG Files

The output directory was inspected with:

```bash
ls -la extracao/jpg
```

The recorded activity result confirms that five image files were recovered.

The exact filenames, individual file sizes, and timestamps were not included in the supplied summary and should be read from the original terminal evidence.

The important result is the presence of five recovered images in the JPEG output directory.

## 5. Expected Results

The activity demonstrates successful extraction of image evidence from the supplied network-related artifact.

| Item | Result |
|---|---|
| Reconstruction Utility | TCPFlow |
| File Carving Utility | Foremost |
| Foremost Input | `imagem.dump` |
| Foremost Output | `extracao` |
| JPEG Output Directory | `extracao/jpg` |
| Recovered Image Count | 5 |

The command:

```bash
ls -la extracao/jpg
```

should display the recovered JPEG files.

## 6. Technical Analysis

### TCPFlow and Packet-Level Analysis

A packet capture contains individual network frames and their protocol fields.

When TCP is used, application data may be segmented across multiple packets.

TCPFlow reconstructs the TCP data stream, making it easier to inspect the transmitted content as a continuous flow.

This is especially useful when application artifacts are distributed across multiple TCP segments.

### Why File Carving Is Relevant

A file transferred over a network may be recoverable from raw captured data even when the original filename or filesystem structure is unavailable.

File carving focuses on recognizable content structures rather than relying exclusively on filesystem metadata.

This makes it a useful complement to network stream reconstruction.

### Foremost Output Structure

The output directory is organized according to the file types recognized by the tool.

The directory:

```text
extracao/jpg
```

contains the JPEG artifacts recovered in the activity.

The number of recovered files is not, by itself, proof that every recovered file is complete or valid.

A forensic examiner should also check:

- Whether each file opens correctly.
- Whether the image content is complete.
- Whether multiple files contain duplicate content.
- Whether the recovered metadata is consistent with the investigation.
- Whether the extraction process introduced truncated or incomplete artifacts.

### Preservation of Source Evidence

The input artifact should not be modified during analysis.

A controlled forensic procedure should preserve the original evidence and perform extraction against a verified copy.

The output directory should be kept separate from the input evidence.

When evidence integrity is relevant, cryptographic hashes can be calculated before and after processing.

## 7. Results and Interpretation

The activity demonstrates the use of TCPFlow and Foremost in network evidence examination.

TCPFlow provides reconstructed TCP data streams, while Foremost performs file carving against the supplied artifact.

The confirmed command:

```bash
foremost -i imagem.dump -o extracao
```

generated an output directory containing the recovered file types.

The subsequent listing:

```bash
ls -la extracao/jpg
```

confirmed the recovery of five JPEG images.

The recovered files represent potential evidence that can be examined and correlated with other artifacts from the network capture.

## 8. Concepts Practiced

- Network forensics
- TCP stream reconstruction
- TCPFlow
- Packet capture analysis
- File carving
- Foremost
- File signatures
- JPEG recovery
- Output directory analysis
- Evidence preservation
- Recovered file validation
- Linux command-line utilities
- `ls -la`

## 9. Evidence

**Required screenshot: Print 3 — PDF page 1.**

The screenshot should show:

```bash
foremost -i imagem.dump -o extracao
```

and the subsequent command:

```bash
ls -la extracao/jpg
```

The terminal should display the personalized prompt and the output confirming five recovered JPEG images.

The screenshot should be legible and show both the extraction operation and the resulting JPEG directory listing.

[View Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 14.1 is on page 1 of the consolidated PDF.

## References

- [TCPFlow — Official Project](https://github.com/simsong/tcpflow)
- [TCPFlow Manual Page](https://man.archlinux.org/man/tcpflow.1.en)
- [Foremost — Kali Linux Tools](https://www.kali.org/tools/foremost/)
- [Foremost — Manual Page](https://www.mankier.com/8/foremost)
- [Foremost — ArchWiki](https://wiki.archlinux.org/title/Foremost)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 14.2](../atividade-14.2-networkminer-imagens/README.md)
