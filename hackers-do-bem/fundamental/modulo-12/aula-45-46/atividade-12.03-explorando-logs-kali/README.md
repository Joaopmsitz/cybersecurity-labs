# Activity 12.03 — Exploring Logs on Kali Linux

## Objective

Explore the main event logging files and tools available on **Kali Linux**, using the `/var/log` directory, the `syslog` file, `journalctl`, and the GNOME **Logs** graphical application.

The activity also demonstrates how to search for occurrences containing the word `error` in system records.

---

## Environment

- **Operating system:** Kali Linux
- **Access:** RDP
- **Log directory:** `/var/log`
- **Tools:** `cat`, `journalctl`, `grep`, and GNOME Logs

---

## 1. Accessing Kali Linux

Kali Linux was started and accessed via RDP.

After logging in, a terminal was opened and administrative privileges were obtained using:

```bash
sudo -i
```

---

## 2. Exploring the `/var/log` Directory

The `/var/log` directory contains various files and directories used by the system to store event records.

To view its contents, the following command was executed:

```bash
ls -l /var/log
```

Output:

```text
total 7652
-rw-r--r--  1 root              root                  0 dez  2 23:00 alternatives.log
-rw-r--r--  1 root              root              73040 nov 27 21:16 alternatives.log.1
-rw-r--r--  1 root              root               6014 jul 10  2024 alternatives.log.2.gz
drwxr-x---  2 root              adm                4096 jul  4  2024 apache2
drwxr-xr-x  2 root              root               4096 dez  2 23:00 apt
drwxr-x---  2 root              adm                4096 jun 11  2024 audit
-rw-r-----  1 root              adm               66442 dez  6 10:47 auth.log
-rw-r-----  1 root              adm               37391 dez  2 23:00 auth.log.1
-rw-r-----  1 root              adm                1395 nov 24 16:30 auth.log.2.gz
-rw-r-----  1 root              adm                1873 out 14  2024 auth.log.3.gz
-rw-r-----  1 root              adm              694409 jul 10  2024 auth.log.4.gz
-rw-------  1 root              root               2590 dez  6 10:45 boot.log
-rw-------  1 root              root             106163 dez  6 10:45 boot.log.1
-rw-------  1 root              root              40417 dez  5 17:40 boot.log.2
-rw-------  1 root              root              44216 dez  3 00:19 boot.log.3
-rw-------  1 root              root              66461 dez  2 23:00 boot.log.4
-rw-------  1 root              root              22404 nov 27 20:41 boot.log.5
-rw-------  1 root              root              25803 nov 24 16:30 boot.log.6
-rw-------  1 root              root              46369 out 14  2024 boot.log.7
-rw-rw----  1 root              utmp                  0 dez  2 23:00 btmp
-rw-rw----  1 root              utmp                  0 nov 24 16:30 btmp.1
drwxr-xr-x  2 clamav            clamav             4096 dez  2 23:00 clamav
-rw-r-----  1 root              adm               27347 dez  6 10:45 cloud-init.log
-rw-r-----  1 root              adm              102475 dez  2 23:00 cloud-init.log.1.gz
-rw-r-----  1 root              adm              105384 dez  2 23:35 cloud-init.log.2.gz
-rw-r-----  1 root              adm              114037 out 14  2024 cloud-init.log.3.gz
-rw-r-----  1 root              adm               97731 dez  6 10:45 cloud-init-output.log
-rw-r-----  1 root              adm               18152 dez  6 10:45 cron.log
-rw-r-----  1 root              adm                7868 dez  2 23:00 cron.log.1
-rw-r-----  1 root              adm                 441 nov 24 16:30 cron.log.2.gz
-rw-r-----  1 root              adm                 621 out 14  2024 cron.log.3.gz
-rw-r--r--  1 root              root                  0 dez  2 23:00 dpkg.log
-rw-r--r--  1 root              root            1398585 nov 27 23:08 dpkg.log.1
-rw-r--r--  1 root              root                764 out 14  2024 dpkg.log.2.gz
-rw-r--r--  1 root              root              94566 jul 10  2024 dpkg.log.3.gz
drwxr-s---  2 Debian-exim       adm                4096 dez  6 10:45 exim4
-rw-r--r--  1 root              root                  0 mai 27  2024 faillog
-rw-r--r--  1 root              root               6216 nov 27 21:08 fontconfig.log
drwxr-xr-x  2 freerad           adm                4096 jul  4  2024 freeradius
drwxr-sr-x+ 3 root              systemd-journal    4096 jul  2  2024 journal
-rw-r-----  1 root              adm              457577 dez  6 10:45 kern.log
-rw-r-----  1 root              adm              208922 dez  2 23:00 kern.log.1
-rw-r-----  1 root              adm               10528 nov 24 16:30 kern.log.2.gz
-rw-r-----  1 root              adm               20605 out 14  2024 kern.log.3.gz
-rw-r-----  1 root              adm               81932 jul 10  2024 kern.log.4.gz
-rw-rw-r--  1 root              utmp             292584 dez  5 22:47 lastlog
drwx--x--x  2 root              root               4096 dez  6 10:45 lightdm
-rw-r-xr-x  2 root              root               4096 mar  2  2024 openvpn
-rw-rwxr-x  2 root              root               4096 dez  2 23:00 postgresql
-rw-------  2 root              root               4096 mai 27  2024 private
lrwxrwxrwx  1 root              root                 39 mai 27  2024 README -> ../../usr/share/doc/systemd/README.logs
drwxr-xr-x  5 root              root               4096 nov 27 20:56 runit
drwx------  2 root              root               4096 mar 13  2024 speech-dispatcher
drwxr-xr-x  2 root              root               4096 jul  1  2024 squid
drwxr-xr-x  2 root              root               4096 dez  5 21:54 suricata
-rw-r-----  1 root              adm             2020220 dez  6 10:47 syslog
-rw-r-----  1 root              adm              976302 dez  2 23:00 syslog.1
-rw-r-----  1 root              adm               32682 nov 24 16:30 syslog.2.gz
-rw-r-----  1 root              adm               70309 out 14  2024 syslog.3.gz
-rw-r-----  1 root              adm              280466 jul 10  2024 syslog.4.gz
drwxr-xr-x  2 root              root               4096 jan 15  2024 sysstat
drwxr-s---  2 debian-tor        adm                4096 jul  4  2024 tor
drwxr-x---  2 root              adm               4096 dez  5 21:54 unattended-upgrades
-rw-r-----  1 root              adm                4400 dez  6 10:45 user.log
-rw-r-----  1 root              adm               15587 dez  2 23:00 user.log.1
-rw-r-----  1 root              adm                 992 nov 24 16:30 user.log.2.gz
-rw-r-----  1 root              root                265 jul  4  2024 vbox-install.log
-rw-r--r--  1 root              root                 37 dez  6 10:45 vbox-setup.log
-rw-r--r--  1 root              root                 37 dez  5 23:08 vbox-setup.log.1
-rw-r--r--  1 root              root                 37 dez  5 22:49 vbox-setup.log.2
-rw-r--r--  1 root              root                 37 dez  5 22:37 vbox-setup.log.3
-rw-r--r--  1 root              root                 37 dez  5 21:46 vbox-setup.log.4
-rw-rw-r--  1 root              utmp             47616 dez  5 22:47 wtmp
-rw-r--r--  1 root              root               8192 dez  5 22:47 wtmp.db
-rw-r-----  1 xrdp              adm               37771 dez  6 10:46 xrdp.log
-rw-r-----  1 xrdp              adm                1778 dez  2 23:00 xrdp.log.1.gz
-rw-r-----  1 xrdp              adm                 1166 nov 24 16:30 xrdp.log.2.gz
-rw-r-----  1 xrdp              adm                 1894 out 14  2024 xrdp.log.3.gz
-rw-r-----  1 xrdp              adm                 1347 jul  4  2024 xrdp.log.4.gz
```

The files and directories observed include records related to authentication, startup, the kernel, services, networking, Docker, Suricata, OpenVPN, user sessions, and other system components.

---

## 3. Exploring `syslog`

The `syslog` file contains general records from various system components and services.

To view its contents, the following command was executed:

```bash
cat /var/log/syslog
```

Part of the displayed output:

```text
2025-12-02T23:00:27.696849-03:00 ip-192-168-98-40 systemd[1]: rsyslog.service: Sent signal SIGHUP to main process 746 (rsyslogd) on client request.
2025-12-02T23:00:27.697808-03:00 ip-192-168-98-40 rsyslogd: [origin software="rsyslogd" swVersion="8.2510.0" x-pid="746" x-info="https://www.rsyslog.com"] rsyslogd was HUPed
2025-12-02T23:00:27.790481-03:00 ip-192-168-98-40 systemd[1]: logrotate.service: Deactivated successfully.
2025-12-02T23:00:27.790791-03:00 ip-192-168-98-40 systemd[1]: Finished logrotate.service - Rotate log files.
2025-12-02T23:00:27.801578-03:00 ip-192-168-98-40 cloud-init[509]: Cloud-init v. 25.3 running 'modules:config' at Wed, 03 Dec 2025 02:00:27 +0000. Up 14.28 seconds.
2025-12-02T23:00:27.869909-03:00 ip-192-168-98-40 sh[1097]: Completed socket interaction for boot stage config

...
```

The output demonstrates that different components can write information to the same log file. In this example, events related to `systemd`, `rsyslogd`, `logrotate`, and `cloud-init` are shown.

---

## 4. Querying the System Journal

In addition to traditional files in `/var/log`, Kali Linux uses the **systemd journal**, which can be queried using the `journalctl` command.

To view records from the current boot, the following command was executed:

```bash
journalctl -b
```

Part of the output:

```text
dez 06 10:45:41 kali kernel: Linux version 6.16.8+kali-cloud-amd64 (devel@kali.org) (x86_64-linux-gnu-gcc->
dez 06 10:45:41 kali kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-6.16.8+kali-cloud-amd64 root=UUID=03b8>
dez 06 10:45:41 kali kernel: BIOS-provided physical RAM map:
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000000100000-0x00000000bffe8fff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000bffe9000-0x00000000bfffffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000e0000000-0x00000000e03fffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000100000000-0x000000013cffffff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x000000013d000000-0x000000013fffffff] reserved
dez 06 10:45:41 kali kernel: printk: legacy bootconsole [earlyser0] enabled
dez 06 10:45:41 kali kernel: NX (Execute Disable) protection: active
dez 06 10:45:41 kali kernel: APIC: Static calls initialized
dez 06 10:45:41 kali kernel: SMBIOS 2.7 present.
dez 06 10:45:41 kali kernel: DMI: Amazon EC2 t3a.medium/, BIOS 1.0 10/16/2017
dez 06 10:45:41 kali kernel: DMI: Memory slots populated: 1/1
dez 06 10:45:41 kali kernel: Hypervisor detected: KVM

...
```

The records show information about the system startup process, including the kernel version, boot parameters, available memory, BIOS information, and detection of the KVM hypervisor.

---

## 5. Searching for Occurrences Using `grep`

To locate lines in `syslog` containing the word `error`, the following command was used:

```bash
grep "error" /var/log/syslog
```

Part of the output:

```text
2025-12-02T23:00:28.076703-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075234187-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.blockfile\"..." error="no scratch file generator: skip plugin" type=io.containerd.snapshotter.v1
2025-12-02T23:00:28.076787-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075518179-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.btrfs\"..." error="path /var/lib/containerd/io.containerd.snapshotter.v1.btrfs (ext4) must be a btrfs filesystem to be used with the btrfs snapshotter: skip plugin" type=io.containerd.snapshotter.v1
2025-12-02T23:00:28.076870-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075568919-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.devmapper\"..." error="devmapper not configured: skip plugin" type=io.containerd.snapshotter.v1
...
```

The command performs a text search for the string `error`. Therefore, finding the word in a line does not necessarily mean that the event has an `error` severity level.

In this case, the displayed lines contain:

```text
level=info
```

The word `error` appears within the details of the `containerd` message, indicating reasons why certain plugins were not loaded.

---

## 6. Accessing the Logs Application

After completing the terminal analysis, the administrative session was ended using:

```bash
exit
```

Next, the following application was opened:

```text
Logs
```

The **Logs** application, also known as **GNOME Logs**, provides a graphical interface for viewing system records.

---

## 7. Exploring GNOME Logs Categories

The application panel displayed categories such as:

- **Important**
- **All**
- **Applications**
- **System**
- **Security**
- **Hardware**

Each category allows users to focus on the display of particular types of records.

### Applications

Displays records related to applications running on the system.

### System

Displays events related to the operating system and its components.

### Security

Focuses on records related to security and activities relevant to system analysis.

### Hardware

Displays events related to devices and hardware components recognized by the system.

---

## 8. Exploring the Security Section

The following category was selected in the **Logs** application:

```text
Security
```

This section displays records related to system security, allowing events that may be relevant during an investigation or analysis of the environment to be observed.

---

## 9. Evidence

The required screenshot for this activity corresponds to **Step 10**, showing the **Security** section of the GNOME **Logs** application.

**Caption to include before the screenshot:**

> Screenshot of Activity 12.03: the `Security` section of the GNOME `Logs` application on Kali Linux, displaying records related to system security.

[**View Evidence — Module 12 / Classes 45–46**](../evidencias.pdf)

---

## Key Concepts

- **`/var/log`:** The traditional directory used by Linux to store log records.
- **`syslog`:** A general log containing events generated by different system components and services.
- **`journalctl`:** A tool for querying the journal maintained by `systemd`.
- **`grep`:** A tool used to search for patterns in text files.
- **GNOME Logs:** A graphical interface for viewing system records.
- **Security log:** A record that can help identify and investigate security-related activities.

## Activity Workflow

```text
Kali Linux
     ↓
/var/log
     ↓
syslog
     ↓
journalctl -b
     ↓
grep "error"
     ↓
GNOME Logs
     ↓
Security
```

## Result

The main logging mechanisms available on Kali Linux were explored, including `/var/log`, `syslog`, `journalctl`, and the GNOME **Logs** application.

A text search for `error` was also performed in `syslog`, and the **Security** category was examined through the graphical interface.

---

[Back to Classes 45–46](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
