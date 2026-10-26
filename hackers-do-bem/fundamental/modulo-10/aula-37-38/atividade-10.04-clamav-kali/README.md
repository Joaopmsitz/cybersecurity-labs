# Activity 10.04 — ClamAV on Kali Linux

## Objective

Install, update, and use ClamAV on Kali Linux to scan files, while also examining the engine version, signature database updates, and antivirus configuration information.

## Environment

- **System:** Kali GNU/Linux Rolling
- **Tool:** ClamAV
- **Version:** 1.4.3
- **Access:** RDP
- **Machine:** Kali Linux
- **Scanned directory:** `/home`

The credentials used to access the lab are not included in this README.

## 1. Opening the Terminal as Root

After accessing the Kali Linux machine, a terminal was opened and the following command was executed:

```bash
sudo -i
```

The terminal was then operating with root privileges.

## 2. Checking the ClamAV Version

The following command was executed:

```bash
clamscan --version
```

**Output:**

```text
ClamAV 1.4.3/27833/Thu Nov 27 06:13:22 2025
```

The output shows the ClamAV engine version and the signature database version initially available in the environment.

## 3. Stopping the Automatic Update Service

Before manually updating the signature database, the `clamav-freshclam` service was stopped:

```bash
systemctl stop clamav-freshclam.service
```

This step helps prevent the automatic update service from conflicting with the manual execution of `freshclam`.

## 4. Updating the Signature Database

The following command was executed:

```bash
freshclam
```

**Output:**

```text
Fri Dec  5 17:43:00 2025 -> ClamAV update process started at Fri Dec  5 17:43:00 2025
Fri Dec  5 17:43:00 2025 -> daily database available for update (local version: 27833, remote version: 27841)
Current database is 8 versions behind.
Downloading database patch # 27834...
Time:    0.1s, ETA:    0.0s [========================>]    1.58KiB/1.58KiB
Downloading database patch # 27835...
Time:    0.0s, ETA:    0.0s [========================>]       791B/791B
Downloading database patch # 27836...
Time:    0.1s, ETA:    0.0s [========================>]    3.39KiB/3.39KiB
Downloading database patch # 27837...
Time:    0.1s, ETA:    0.0s [========================>]    2.18KiB/2.18KiB
Downloading database patch # 27838...
Time:    0.1s, ETA:    0.0s [========================>]      1023B/1023B
Downloading database patch # 27839...
Time:    0.1s, ETA:    0.0s [========================>]    3.99KiB/3.99KiB
Downloading database patch # 27840...
Time:    0.1s, ETA:    0.0s [========================>]    4.57KiB/4.57KiB
Downloading database patch # 27841...
Time:    0.1s, ETA:    0.0s [========================>]       790B/790B
Fri Dec  5 17:43:03 2025 -> Testing database: '/var/lib/clamav/tmp.6ea2feafb0/clamav-a484adb123cfedf1746b313bb5ea45b2.tmp-daily.cld' ...
Fri Dec  5 17:43:13 2025 -> Database test passed.
Fri Dec  5 17:43:13 2025 -> daily.cld updated (version: 27841, sigs: 2077269, f-level: 90, builder: svc.clamav-publisher)
Fri Dec  5 17:43:13 2025 -> main.cvd database is up-to-date (version: 62, sigs: 6647427, f-level: 90, builder: sigmgr)
Fri Dec  5 17:43:13 2025 -> bytecode.cld database is up-to-date (version: 339, sigs: 80, f-level: 90, builder: nrandolp)
WARNING: Fri Dec  5 17:43:13 2025 -> Clamd was NOT notified: Can't connect to clamd through /var/run/clamav/clamd.ctl: No such file or directory
```

The `daily.cld` database was updated from version `27833` to `27841`, an increase of eight versions.

The new database passed its validation test:

```text
Database test passed.
```

A warning also indicated that `clamd` was not notified because the socket `/var/run/clamav/clamd.ctl` was unavailable. This did not prevent the signature database from being updated successfully.

## 5. Scanning the `/home` Directory

After updating the database, the following command was executed:

```bash
clamscan -r /home
```

The `-r` option enables recursive scanning, allowing ClamAV to process the directories and subdirectories found under `/home`.

Part of the output displayed during the scan:

```text
┌──(root㉿kali)-[~]
└─# clamscan -r /home
Loading:    21s, ETA:   0s [========================>]    8.71M/8.71M sigs
Compiling:   5s, ETA:   0s [========================>]       41/41 tasks

/home/aluno/.zshrc: OK
/home/aluno/.xsession-errors: OK
/home/aluno/.local/share/nautilus/scripts/Terminal: OK
/home/aluno/.local/share/keyrings/login.keyring: OK
/home/aluno/.local/share/keyrings/user.keystore: OK
/home/aluno/.local/share/xrdp/xrdp-chansrv.10.log: OK
/home/aluno/.local/share/torbrowser/tbb/x86_64/tor-browser/start-tor-browser.desktop: OK

...

----------- SCAN SUMMARY -----------
Known viruses: 8708962
Engine version: 1.4.3
Scanned directories: 1015
Scanned files: 6128
Infected files: 0
Data scanned: 1319.81 MB
Data read: 1553.00 MB (ratio 0.85:1)
Time: 583.507 sec (9 m 43 s)
Start Date: 2025:12:05 17:45:28
End Date:   2025:12:05 17:55:12
```

ClamAV recursively scanned the `/home` directory.

The most important results from the summary were:

```text
Scanned directories: 1015
Scanned files: 6128
Infected files: 0
Data scanned: 1319.81 MB
Data read: 1553.00 MB (ratio 0.85:1)
Time: 583.507 sec (9 m 43 s)
```

No files were identified as infected by ClamAV during this scan.

### Evidence — Step 5

**Caption to include before the screenshot:**

> Screenshot of Activity 10.04: the results of the recursive scan of the `/home` directory performed by ClamAV, including the `SCAN SUMMARY` with the number of files analyzed and the infection detection results.

[View Evidence — Classes 37–38](../evidencias.pdf)

## 6. Analyzing the Scan Summary

After `clamscan` finished, the information displayed in the `SCAN SUMMARY` was reviewed.

The main results were:

| Information | Result |
|---|---|
| Engine version | 1.4.3 |
| Directories scanned | 1015 |
| Files scanned | 6128 |
| Infected files | 0 |
| Data scanned | 1319.81 MB |
| Data read | 1553.00 MB |
| Execution time | 9 min 43 sec |

## 7. Checking ClamAV Configuration

The following command was executed:

```bash
clamconf
```

The command displayed the configuration settings available in the environment, along with information about the engine and signature databases.

Relevant output:

```text
Checking configuration files in /etc/clamav

Config file: clamd.conf
-----------------------
AlertExceedsMax disabled
CacheSize = "65536"
PreludeEnable disabled
PreludeAnalyzerName = "ClamAV"
LogFile = "/var/log/clamav/clamav.log"
LogFileUnlock disabled
LogFileMaxSize = "9223372036854775807"
LogTime = "yes"
LogClean disabled

...

clamav-milter.conf not found

Software settings
-----------------
Version: 1.4.3
Optional features supported: MEMPOOL AUTOIT_EA06 ICONV

Database information
--------------------
Database directory: /var/lib/clamav
bytecode.cld: version 339, sigs: 80, built on Thu Sep 11 09:29:19 2025
main.cvd: version 62, sigs: 6647427, built on Thu Sep 16 09:32:42 2021
daily.cld: version 27841, sigs: 2077269, built on Fri Dec  5 06:23:11 2025
Total number of signatures: 8724776

Platform information
--------------------
uname: Linux 6.16.8+kali-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.16.8-1kali1 (2025-09-24) x86_64
OS: Linux, ARCH: x86_64, CPU: x86_64
Full OS version: Kali GNU/Linux Rolling
zlib version: 1.3.1 (1.3.1), compile flags: a9
platform id: 0x0a21d5d508000000000e0300

Build information
-----------------
GNU C: 14.3.0
sizeof(void*) = 8
Engine flevel: 213, dconf: 213
```

The output confirmed, among other details, that:

- The installed ClamAV engine version was `1.4.3`.
- The `daily.cld` database was at version `27841` after the update.
- The database directory was `/var/lib/clamav`.
- The reported total was `8,724,776` signatures.
- The operating system was Kali GNU/Linux Rolling, running on the `x86_64` architecture.

## 8. Closing the Activity

After reviewing the ClamAV configuration, the activity was completed.

## Key Concepts

- **ClamAV:** An open-source antivirus engine used to detect malware.
- **Freshclam:** A tool responsible for updating ClamAV signature databases.
- **Clamscan:** A command-line utility used to scan files and directories.
- **Signatures:** Data used by the detection engine to identify known threats.
- **Recursive scan:** A scan that processes a directory and its subdirectories.

## Activity Workflow

```text
Check the version
      ↓
Stop automatic updates
      ↓
Update signatures
      ↓
Scan /home
      ↓
Analyze the SCAN SUMMARY
      ↓
Review the configuration
```

## Result

ClamAV was updated and used to recursively scan the `/home` directory.

A total of 6,128 files were scanned, and no infected files were detected during the scan.

---

[Back to Classes 37–38](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
