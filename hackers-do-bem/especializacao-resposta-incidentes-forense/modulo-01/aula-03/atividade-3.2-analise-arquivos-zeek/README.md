# Activity 3.2 — File Analysis with Zeek

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 03
> **Environment:** forenseLinux VM
> **Status:** Completed

## Objective

Configure the Zeek File Analysis Framework to generate SHA256 hashes for files observed in network traffic.

## Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tool | Zeek |
| Framework | File Analysis Framework |
| Main Configuration | /opt/zeek/share/zeek/site/local.zeek |
| Custom Script | hash_sha256.zeek |

## Procedure

### 1. Enable Existing File Analysis Features

Edit the local configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

The exercise includes the following directives:

```zeek
# Enable MD5 and SHA1 hashing for all files.
@load frameworks/files/hash-all-files

# Detect SHA1 sums in Team Cymru's Malware Hash Registry.
@load frameworks/files/detect-MHR
```

### 2. Create the SHA256 Script

Create the custom script:

```bash
sudo nano /opt/zeek/share/zeek/site/hash_sha256.zeek
```

Script content:

```zeek
##! Performs SHA256 hashing on all files.

@load base/files/hash

event file_new(f: fa_file)
    {
    Files::add_analyzer(f, Files::ANALYZER_SHA256);
    }
```

### 3. Load the Custom Script

Edit the local configuration again:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Add the following directive:

```zeek
# Enable SHA256 hashing for files
@load hash_sha256
```

The custom script is loaded by the main Zeek site configuration.

### 4. Apply the Changes

Stop the running service:

```bash
sudo /opt/zeek/bin/zeekctl stop
```

Deploy the updated configuration:

```bash
sudo /opt/zeek/bin/zeekctl deploy
```

## Technical Analysis

The File Analysis Framework enables Zeek to identify and analyze files observed in network traffic.

The activity combines existing MD5 and SHA1 hashing capabilities with a custom SHA256 analyzer.

The Team Cymru Malware Hash Registry integration allows supported file hashes to be checked against known malware intelligence.

## Result

The activity report records the creation of the SHA256 script and its inclusion in local.zeek.

This configuration enables the additional SHA256 file analysis capability during Zeek processing.

## Concepts Practiced

- Zeek scripting
- File Analysis Framework
- Cryptographic hashing
- MD5, SHA1, and SHA256
- Malware Hash Registry integration
- Configuration file management
- Custom analyzer deployment

## Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

---

[Back to Class 03](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
