# Activity 2.07 — Analyzing Linux System Events with Logcheck

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 07–08  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use Logcheck to analyze events recorded by a Linux system, focusing on authentication activity, network services, and error messages.

This activity demonstrates how a monitoring tool can filter and report relevant system log events, helping identify behavior that may require further investigation.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** Logcheck
- **Data sources:** System log files
- **Administrative context:** Root session

## Procedure

### 1. Run Logcheck

Logcheck was executed using its service account:

```bash
sudo -u logcheck logcheck -o -t
```

The execution produced events related to `sudo`, the DHCP client, and the XRDP service:

```text
This email is sent by logcheck. If you no longer wish to receive
such mail, you can either uninstall the logcheck package or modify
its configuration file (/etc/logcheck/logcheck.conf).

Security Events for sudo
=-=-=-=-=-=-=-=-=-=-=-=-
2024-02-08T18:04:35.855136-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
fev 08 18:04:35 kali sudo[5209]: pam_unix(sudo-i:session): session closed for user root

System Events
=-=-=-=-=-=-=
2024-02-08T18:02:53.499503-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
2024-02-08T18:04:42.410794-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
2024-02-08T18:04:50.231955-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:04:50.239116-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:02:53 kali dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
fev 08 18:04:42 kali dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
fev 08 18:04:50 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:04:50 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
```

The output included a security event associated with the closing of a root session, DHCP client requests on `eth0`, and XRDP clipboard-related errors.

### 2. Change the Logcheck Configuration

An administrative shell was opened:

```bash
sudo -i
```

The configuration file was opened with Nano:

```bash
nano /etc/logcheck/logcheck.conf
```

The configuration used during the activity included:

```bash
REPORTLEVEL="workstation"

SENDMAILTO="<email address configured in the lab>"

MAILASATTACH=1
```

The email address configured during the laboratory exercise is not reproduced in this document.

The `REPORTLEVEL` setting determines which filtering rules Logcheck uses when preparing its reports.

The levels discussed during the activity were:

| Level | Description |
|---|---|
| `server` | Default level for systems running services and daemons |
| `paranoid` | More restrictive and detailed reporting, potentially generating more events |
| `workstation` | Filtering profile intended for workstation environments |

The setting used in the exercise was:

```bash
REPORTLEVEL="workstation"
```

### 3. Run Logcheck Again

After modifying the configuration, Logcheck was executed again:

```bash
sudo -u logcheck logcheck -o -t
```

The second execution displayed additional events related to `sudo` sessions, along with the previously observed network and XRDP events:

```text
This email is sent by logcheck. If you no longer wish to receive
such mail, you can either uninstall the logcheck package or modify
its configuration file (/etc/logcheck/logcheck.conf).

Security Events for sudo
=-=-=-=-=-=-=-=-=-=-=-=-
2024-02-08T18:04:35.855136-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
2024-02-08T18:12:31.367745-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
2024-02-08T18:16:03.554902-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
fev 08 18:12:31 kali sudo[8454]: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
fev 08 18:16:03 kali sudo[8454]: pam_unix(sudo-i:session): session closed for user root

System Events
=-=-=-=-=-=-=
2024-02-08T18:02:53.499503-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
2024-02-08T18:04:42.410794-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
2024-02-08T18:04:50.231955-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:04:50.239116-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:06:48.170853-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 114710ms.
2024-02-08T18:08:42.922879-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 112740ms.
2024-02-08T18:10:35.763167-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 129930ms.
2024-02-08T18:12:45.793377-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 129080ms.
2024-02-08T18:13:47.104704-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:13:47.111981-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:14:54.973652-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 114690ms.
fev 08 18:08:42 kali dhclient[495]: XMT: Solicit on eth0, interval 112740ms.
fev 08 18:10:35 kali dhclient[495]: XMT: Solicit on eth0, interval 129930ms.
fev 08 18:12:45 kali dhclient[495]: XMT: Solicit on eth0, interval 129080ms.
fev 08 18:13:47 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:13:47 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:14:54 kali dhclient[495]: XMT: Solicit on eth0, interval 114690ms.
```

The second report contained additional authentication records, including the opening and closing of an administrative session.

### 4. Analyze the Events

The second execution provided more detail about system activity during the period represented by the logs.

#### Authentication Events

The `sudo` records showed the opening and closing of an administrative session:

```text
sudo: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
sudo: pam_unix(sudo-i:session): session closed for user root
```

These events are useful during security investigations because they help establish when administrative privileges were used.

The records show that a session associated with the `root` account was opened by a process associated with UID `1001` and subsequently closed.

#### DHCP Events

The following messages appeared repeatedly:

```text
dhclient[495]: XMT: Solicit on eth0, interval 108860ms
```

These messages indicate that the DHCP client was transmitting solicitation requests on the `eth0` network interface.

Such events may be expected during network configuration or address acquisition. Their significance depends on the system's network state and configuration.

#### XRDP Events

The logs contained the following errors:

```text
xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
```

These messages originated from the XRDP channel server component and indicated that a clipboard selection request used an unrecognized target.

In the laboratory context, these events were observed during remote-session use. They were not treated as a security incident based solely on the presence of the `[ERROR]` label.

### 5. Concepts Practiced

#### Logcheck

Logcheck is a tool used to analyze and filter log events, highlighting messages that may be relevant to system administration and security monitoring.

#### Log Analysis

Log analysis is important for identifying:

- Authentication activity and privilege usage
- Administrative actions and system changes
- Network events
- Service errors
- Unusual behavior
- Potential indicators of compromise

#### Monitoring and Detection

Logcheck supports detection by filtering system log information, reducing the need to manually review every recorded event.

It does not replace investigation or other security monitoring controls.

#### Sudo and PAM

The `sudo` events in this activity included messages generated by PAM (Pluggable Authentication Modules), which participates in authentication and session management.

These records can help analysts reconstruct administrative activity.

#### DHCP

The `dhclient` process interacts with DHCP services to obtain or renew network configuration information.

#### XRDP

XRDP provides remote graphical access to Linux systems. Its components can generate session-related events, including errors involving features such as clipboard integration.

## Commands Used

The main commands used during the activity were:

```bash
sudo -u logcheck logcheck -o -t

sudo -i

nano /etc/logcheck/logcheck.conf

sudo -u logcheck logcheck -o -t
```

The configuration file was updated with the following settings:

```bash
REPORTLEVEL="workstation"

SENDMAILTO="<email address configured in the lab>"

MAILASATTACH=1
```

## Interpreting the Results

The activity demonstrated the use of Logcheck to filter and present Linux system log events.

The first execution displayed a root-session closure, DHCP requests, and XRDP clipboard errors. After the configuration was changed to use the `workstation` report level, the second execution included additional `sudo` session events and further network and XRDP records.

The results highlighted the importance of reviewing logs in context. For example:

- A `sudo` session opening or closing can help establish an administrative activity timeline.
- DHCP solicitation messages can reflect routine network behavior.
- XRDP clipboard errors may arise from remote-session compatibility or clipboard handling issues.

A log message marked `[ERROR]` does not automatically indicate a security incident. Events should be correlated with other information, system configuration, and the activities performed at the time.

## Result

The activity demonstrated how Logcheck can filter and report Linux system events.

The exercise provided practical experience in observing:

- Administrative session opening and closing events
- DHCP solicitation messages on a network interface
- XRDP clipboard-related errors
- The effect of the `REPORTLEVEL` setting on Logcheck reporting
- The importance of contextual interpretation during log analysis

The exercise reinforced the role of log analysis in system monitoring and security-event investigation.

## Concepts Practiced

- Logcheck
- Linux log analysis
- System event monitoring
- Authentication and privilege auditing
- `sudo` and PAM
- DHCP and network events
- XRDP session events
- Log filtering and report levels
- Security-event interpretation
- Detection and incident investigation

## Evidence

The activity evidence is included in the PDF for Classes 07–08.

The screenshot requested by the activity corresponds to **Step 5**, as specified by the laboratory instructions.

[View Evidence — Classes 07–08](../evidencia.pdf)

---

[Back to Classes 07–08](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
