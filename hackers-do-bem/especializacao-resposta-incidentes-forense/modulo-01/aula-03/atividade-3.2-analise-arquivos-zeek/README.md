# Activity 3.2 — File Analysis and SHA256 Hashing with Zeek

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Configure the Zeek File Analysis Framework to calculate MD5, SHA1, and SHA256 hashes for files observed in network traffic.

The activity also introduces integration with the Team Cymru Malware Hash Registry (MHR), which can identify hashes associated with known malware.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Framework | File Analysis Framework |
| Main Configuration | /opt/zeek/share/zeek/site/local.zeek |
| Custom Script | /opt/zeek/share/zeek/site/hash_sha256.zeek |
| Hash Algorithms | MD5, SHA1, SHA256 |
| Malware Intelligence | Team Cymru MHR |

## 3. File Analysis Framework

The Zeek File Analysis Framework supports file-related security and forensic operations, including:

- Automatic file hashing.
- File type identification.
- MIME type inspection.
- Malware hash identification.
- File extraction.
- File metadata analysis.
- File transfer correlation.
- Recording files observed in network traffic.

The framework provides a generalized way to analyze files regardless of the network protocol used to transfer them.

## 4. Procedure

### Step 1 — Enable MD5, SHA1, and Malware Hash Registry Detection

Edit the main site configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

The activity material specifies loading the following scripts:

```zeek
# Enable MD5 and SHA1 hashing for all files.
@load frameworks/files/hash-all-files

# Detect SHA1 sums in Team Cymru's Malware Hash Registry.
@load frameworks/files/detect-MHR
```

The `@load` directive instructs Zeek to load a script or policy module.

The first script enables file hashing capabilities for the configured algorithms.

The second integrates the file hash analysis with Team Cymru's Malware Hash Registry.

Save and exit Nano with:

- `Ctrl + O`
- `Enter`
- `Ctrl + X`

### Step 2 — Create the Custom SHA256 Script

The assignment explains that SHA256 hashing is not automatically enabled by the configuration already presented.

Create the custom script:

```bash
sudo nano /opt/zeek/share/zeek/site/hash_sha256.zeek
```

Insert the following code:

```zeek
##! Realiza o hashing SHA256 em todos os arquivos.

@load base/files/hash

event file_new(f: fa_file)
    {
    Files::add_analyzer(f, Files::ANALYZER_SHA256);
    }
```

The script contains the following components:

| Component | Function |
|---|---|
| `@load base/files/hash` | Loads the file hashing framework |
| `event file_new(f: fa_file)` | Executes when Zeek observes a new file |
| `Files::add_analyzer()` | Attaches an analyzer to the file |
| `Files::ANALYZER_SHA256` | Enables SHA256 analysis |

Save the file:

- `Ctrl + O`
- `Enter`
- `Ctrl + X`

### Step 3 — Load the SHA256 Script in local.zeek

Edit the main site configuration again:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add the following lines after the last existing configuration directive:

```zeek
# Inclui o hash SHA256 para os arquivos
@load hash_sha256
```

This directive loads the custom script created in the previous step.

The configuration now includes the existing MD5 and SHA1 policies, the Team Cymru integration, and the additional SHA256 analyzer.

Save and exit Nano.

### Step 4 — Stop the Running Service

Stop Zeek before applying the updated configuration:

```bash
sudo /opt/zeek/bin/zeekctl stop
```

### Step 5 — Apply the New Configuration

Deploy the updated configuration:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

This applies the new file analysis configuration.

## 5. Configuration Summary

The relevant configuration directives are:

```zeek
# Enable MD5 and SHA1 hashing for all files.
@load frameworks/files/hash-all-files

# Detect SHA1 sums in Team Cymru's Malware Hash Registry.
@load frameworks/files/detect-MHR

# Enable custom SHA256 hashing.
@load hash_sha256
```

Custom script:

```zeek
##! Realiza o hashing SHA256 em todos os arquivos.

@load base/files/hash

event file_new(f: fa_file)
    {
    Files::add_analyzer(f, Files::ANALYZER_SHA256);
    }
```

## 6. Results

The activity report records that the custom `hash_sha256.zeek` script was created and that `@load hash_sha256` was added to `local.zeek`.

The updated configuration was applied through ZeekControl.

The subsequent activity demonstrates the resulting file metadata and hashing information in Zeek records.

The example hash values and JSON output are documented in Activity 3.3 and Activity 3.5, where the corresponding records are presented.

## 7. Technical Interpretation

Cryptographic hashes allow analysts to identify files using fixed-length digests derived from their contents.

| Algorithm | Application |
|---|---|
| MD5 | File identification and legacy integrity checks |
| SHA1 | File identification and malware hash lookups |
| SHA256 | Stronger file fingerprinting for security analysis |

A matching hash can support the identification of a known file or known malware sample.

A hash match should be interpreted together with contextual information such as the file source, network connection, MIME type, and security intelligence.

The Team Cymru integration uses file hash information to query its Malware Hash Registry and can generate Zeek notices when a match is identified.

## 8. Concepts Practiced

- Zeek File Analysis Framework
- Custom Zeek scripts
- File event handling
- MD5 and SHA1 hashing
- SHA256 analyzer configuration
- Malware Hash Registry integration
- Site configuration management
- Service redeployment

## 9. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot corresponds to Step 2 of the original assignment and documents the edited `local.zeek` configuration containing the `@load hash_sha256` directive.

## References

- [Zeek File Analysis Framework](https://docs.zeek.org/en/current/frameworks/file-analysis.html)
- [Zeek Script Index](https://docs.zeek.org/en/current/reference/zeekscript/scripts.html)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../../README.md)
