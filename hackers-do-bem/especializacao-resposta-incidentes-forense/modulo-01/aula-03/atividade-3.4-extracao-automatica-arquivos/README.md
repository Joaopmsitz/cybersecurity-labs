# Activity 3.4 — Automatic File Extraction

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Configure Zeek to automatically extract selected file types from observed network traffic and store the extracted files in a dedicated directory.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Framework | File Extraction |
| Configuration | /opt/zeek/share/zeek/site/file-extraction/config.zeek |
| Extraction Directory | /opt/zeek/extract_files |
| Network Interface | ens5 |

## Procedure

### 1. Configure the Extraction Framework

Edit:

```bash
sudo nano /opt/zeek/share/zeek/site/file-extraction/config.zeek
```

Configure the extraction directory and load the common exploit-type plugin:

```zeek
module FileExtraction;

# Directory used to store extracted files
redef path = "/opt/zeek/extract_files/";

# Load common file extraction policies
@load ./plugins/extract-common-exploit-types
```

### 2. Create the Extraction Directory

Execute:

```bash
sudo mkdir /opt/zeek/extract_files
```

### 3. Update the Main Configuration

Edit:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add the configuration directives:

```zeek
# Disable checksum validation due to VM NIC checksum offloading
redef ignore_checksums = T;

# Load installed Zeek packages
@load packages
```

### 4. Deploy the Configuration

Apply the changes:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

Installed and loaded packages can be inspected using:

```bash
sudo /opt/zeek/bin/zkg list installed
sudo /opt/zeek/bin/zkg list loaded
```

### 5. Identify the Network Interface

Execute:

```bash
ip addr
```

The activity uses `ens5` as the network interface for the capture example.

### 6. Capture Traffic and Extract Files

Start Zeek with the file extraction policy:

```bash
sudo /opt/zeek/bin/zeek -C -i ens5 /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```

The expected startup message includes:

```text
listening on ens5
```

Keep the capture process running.

In another terminal, download the sample PDF used by the exercise:

```bash
cd /opt/zeek
sudo wget http://ftp4.freebsd.org/pub/FreeBSD/doc/en/books/faq/faq_en.pdf
```

Inspect the extraction directory:

```bash
cd /opt/zeek/extract_files/
ls -la
```

The extracted files can be inspected with:

```bash
sudo file extract-*HTTP*
```

## Result

The activity report records that Zeek captured network traffic through `ens5` and automatically extracted a PDF downloaded during the test.

## Concepts Practiced

- Automatic file extraction
- Zeek File Extraction Framework
- Network interface identification
- Live traffic monitoring
- File classification
- Extracted artifact inspection
- Network-based forensic evidence collection

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
