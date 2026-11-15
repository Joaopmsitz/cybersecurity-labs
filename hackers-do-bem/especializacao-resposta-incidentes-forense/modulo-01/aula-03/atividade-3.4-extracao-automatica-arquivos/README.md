# Activity 3.4 — Automatic File Extraction with Zeek

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Configure the Zeek File Extraction Framework to automatically extract selected files observed in network traffic and store them in a designated directory.

The activity demonstrates how a network monitoring sensor can preserve file artifacts for subsequent security analysis and forensic investigation.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Package Manager | zkg |
| File Extraction Configuration | /opt/zeek/share/zeek/site/file-extraction/config.zeek |
| Main Site Configuration | /opt/zeek/share/zeek/site/local.zeek |
| Extraction Directory | /opt/zeek/extract_files/ |
| Network Interface | ens5 |
| Test File | faq_en.pdf |

## 3. Procedure

### Step 1 — Configure the File Extraction Package

Open the extraction configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/file-extraction/config.zeek
```

Locate:

```zeek
module FileExtraction;
```

Configure the extraction directory and load the common exploit-type extraction plugin:

```zeek
module FileExtraction;

#### Extracao automatica de arquivos

# A linha a seguir configura onde os arquivos extraidos serao armazenados
redef path = "/opt/zeek/extract_files/";

# A linha a seguir configura 'plugins' que podem ser carregados
# estes sao modulos de atalho para especificar
# politicas comuns de extracao de arquivos. Exemplo:
# @load ./plugins/extract-pe.bro
@load ./plugins/extract-common-exploit-types
```

Save the configuration:

- `Ctrl + O`
- `Enter`
- `Ctrl + X`

The configured path determines where the package stores extracted files.

The plugin provides a collection of common extraction policies for selected file types, including executable and document formats.

### Step 2 — Create the Extraction Directory

Create the directory configured in the previous step:

```bash
sudo mkdir /opt/zeek/extract_files
```

Check the directory if needed:

```bash
ls -ld /opt/zeek/extract_files
```

The second command is an additional verification command; its output was not preserved in the activity report.

### Step 3 — Enable Package Loading and Checksum Configuration

If this is the first installation of a Zeek package in the environment, edit:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add the following lines at the end:

```zeek
# Desativa checagem de checksum pois o NIC da VM faz checksum offloading
redef ignore_checksums = T;

# Carregar Pacotes Zeek
@load packages
```

The first directive disables checksum validation for the monitored traffic, as required by the VM NIC checksum offloading configuration described in the assignment.

The second directive loads the installed Zeek packages.

The assignment notes that this configuration is required only once for the package-loading setup.

Save and exit Nano.

### Step 4 — Deploy the Configuration

Apply the new configuration and start the managed Zeek service:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

The `deploy` operation applies the modified configuration.

#### Verify Installed Packages

List installed packages:

```bash
sudo /opt/zeek/bin/zkg list installed
```

List loaded packages:

```bash
sudo /opt/zeek/bin/zkg list loaded
```

These commands help identify which packages are installed and which packages are loaded by Zeek.

No specific package-listing output was preserved in the activity report.

### Step 5 — Identify the Network Interface

Execute:

```bash
ip addr
```

The exercise describes two interfaces in its example output:

- `lo` — loopback interface.
- `ens5` — network interface selected for traffic monitoring.

The selected interface for the subsequent example is:

```text
ens5
```

The actual interface name should be verified in the target environment before starting the capture.

### Step 6 — Start Network Capture and Extract Files

The following operation requires two terminal windows. Both steps must be executed.

#### A. Start Zeek Packet Capture

Execute in the first terminal:

```bash
sudo /opt/zeek/bin/zeek -C -i ens5 /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```

Command components:

| Parameter | Function |
|---|---|
| `-C` | Ignores checksum validation |
| `-i ens5` | Selects the network interface |
| `extract-all-files.zeek` | Loads the policy to extract observed files |

The expected startup output in the assignment is:

```text
listening on ens5
```

Keep this terminal running so that Zeek continues capturing traffic.

#### B. Generate Test Network Traffic

Open a second terminal and execute:

```bash
cd /opt/zeek
```

Download the sample PDF specified in the activity:

```bash
sudo wget http://ftp4.freebsd.org/pub/FreeBSD/doc/en/books/faq/faq_en.pdf
```

Navigate to the extraction directory:

```bash
cd /opt/zeek/extract_files/
```

List the extracted files:

```bash
ls -la
```

The assignment explains that an extracted artifact may receive a name similar to:

```text
extract-1689972451.888597-HTTP-FRY1likphLoEL2en6
```

This is an example filename from the training material, not a claim that the student's PDF had exactly that filename.

#### C. Inspect the Extracted File

List the available files:

```bash
ls -l
```

Identify the HTTP extraction artifact:

```bash
sudo file extract-*HTTP*
```

Open the extracted file using its actual filename:

```bash
sudo nano extract-1689972451.888597-HTTP-FRY1likphLoEL2en6
```

Replace the example filename with the file generated in the environment.

## 4. Expected Outputs and Observations

### Capture Startup

The assignment provides:

```text
listening on ens5
```

This confirms that Zeek started capturing traffic on the selected interface.

### Extraction Directory

The assignment explains that a file with an HTTP-related extraction name should appear in:

```text
/opt/zeek/extract_files/
```

The exact output of `ls -la` depends on the traffic observed during the exercise.

A delay may occur before the file becomes visible.

The training material recommends using the capture startup screenshot as the required evidence when the extraction output has not yet appeared.

## 5. Results

The activity report records that the extraction directory was configured and that Zeek captured network traffic on the `ens5` interface.

A PDF was downloaded during the test, and the report states that Zeek successfully extracted the downloaded file.

The configured extraction directory was:

```text
/opt/zeek/extract_files/
```

No specific extracted filename from the student's execution was preserved in the written report.

## 6. Technical Interpretation

Automatic file extraction allows network traffic monitoring to produce local file artifacts for further investigation.

This capability supports tasks such as:

- Preserving suspicious files for analysis.
- Calculating cryptographic hashes.
- Inspecting MIME types and file metadata.
- Correlating files with network connections.
- Providing artifacts for malware analysis.
- Supporting incident response and forensic documentation.

The difference between file observation and extraction is important: a file record may exist in files.log even when its content was not written to disk.

## 7. Troubleshooting and Packet Loss

The assignment recommends checking packet capture statistics if extracted files do not appear.

Execute:

```bash
sudo /opt/zeek/bin/zeekctl netstats
```

The `dropped` column reports packets discarded by the monitored sensor.

A significant packet-loss count can affect file reconstruction and extraction.

Additional diagnostic information may be available in:

```text
/opt/zeek/logs/current/reporter.log
```

The assignment recommends investigating:

- Packet capture completeness.
- Packet loss.
- Sensor performance.
- Network interface capacity.
- Hardware resources.
- Zeek reporter messages.

## 8. Path Distinction

The activity's configured extraction directory is:

```text
/opt/zeek/extract_files/
```

The later illustrative malware scenario in Activity 3.5 uses a different example path:

```text
/opt/zeek/extracted/
```

These paths are preserved as presented in their respective parts of the training material. They should not be treated as evidence that both directories were configured identically in the student's VM.

## 9. Concepts Practiced

- File extraction framework
- Zeek package configuration
- zkg package manager
- Network interface identification
- Packet capture
- HTTP file transfer monitoring
- File preservation
- Artifact inspection
- Network monitoring troubleshooting
- Packet-loss analysis

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot corresponds to Step 6. The original assignment requires both capture and download operations to be performed, but allows the screenshot to show either:

- Zeek listening on `ens5`.
- The extracted file in the extraction directory.

The activity report records successful PDF extraction during the test.

## References

- [Zeek File Analysis Framework](https://docs.zeek.org/en/current/frameworks/file-analysis.html)
- [Zeek extract-all-files Policy](https://docs.zeek.org/en/current/scripts/policy/frameworks/files/extract-all-files.zeek.html)
- [Zeek files.log Reference](https://docs.zeek.org/en/current/reference/logs/files.html)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
