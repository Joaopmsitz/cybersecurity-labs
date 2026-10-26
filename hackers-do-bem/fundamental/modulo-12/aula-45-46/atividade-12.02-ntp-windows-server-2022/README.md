# Activity 12.02 — Enabling NTP on Windows Server 2022

## Objective

Configure the Windows Time (W32Time) service on Windows Server 2022 to use NTP (Network Time Protocol), enabling the NTP server and client through Group Policy and configuring the server `time.google.com`.

At the end of the activity, the service status is queried using the command `w32tm /query /status`.

## Environment

- **Operating system:** Windows Server 2022
- **Access:** RDP
- **Service:** Windows Time (W32Time)
- **Protocol:** NTP
- **Configured NTP server:** `time.google.com`

## 1. Opening the Group Policy Editor

In the Windows Server 2022 taskbar search field, the following command was entered:

```text
gpedit.msc
```

The Local Group Policy Editor was then opened.

## 2. Accessing Windows Time Settings

In the Group Policy Editor, the following path was followed:

```text
Computer Configuration
→ Administrative Templates
→ System
→ Windows Time Service
→ Time Providers
```

The Time Providers section contains settings related to the time providers used by Windows.

## 3. Enabling the Windows NTP Server

In the right pane of the window, the following policy was located:

```text
Enable Windows NTP Server
```

The policy was opened by double-clicking it.

Next, the following actions were performed:

- Selected **Enabled**.
- Clicked **OK**.

This setting enables the Windows NTP server functionality.

## 4. Enabling the Windows NTP Client

In the same section, the following policy was located:

```text
Enable Windows NTP Client
```

The policy was opened and configured as follows:

```text
Enabled
```

Then, **OK** was clicked.

This setting enables the Windows NTP client to synchronize the system clock.

## 5. Configuring the NTP Server

Still in Time Providers, the following policy was opened:

```text
Configure Windows NTP Client
```

The setting was configured as follows:

```text
Enabled
```

In the `NtpServer` field, the following value was entered:

```text
time.google.com,0x9
```

Then, **OK** was clicked.

The value `time.google.com` specifies the reference server configured for the NTP client. The parameter `0x9` is part of the Windows Time provider configuration.

## 6. Opening PowerShell as Administrator

In the taskbar search field, the following term was entered:

```text
Windows PowerShell
```

Next, Windows PowerShell was right-clicked, and the following option was selected:

```text
Run as administrator
```

## 7. Restarting the Windows Time Service

To apply the settings to the service, the following command was executed:

```powershell
net stop w32time
```

Output:

```text
PS C:\Users\Administrator> net stop w32time
The Windows Time service is stopping.
The Windows Time service was stopped successfully.
```

The service was successfully stopped.

## 8. Starting Windows Time Again

Next, the service was started again:

```powershell
net start w32time
```

Output:

```text
PS C:\Users\Administrator> net start w32time
The Windows Time service is starting.
The Windows Time service was started successfully.
```

The Windows Time service resumed operation.

## 9. Querying the NTP Service Status

To check the current status of the time service, the following command was executed:

```powershell
w32tm /query /status
```

The output provided by the lab was:

```text
PS C:\Users\Administrator> w32tm /query /status
Leap Indicator: 0(no warning)
Stratum: 1 (primary reference - syncd by radio clock)
Precision: -23 (119.209ns per tick)
Root Delay: 0.0000000s
Root Dispersion: 10.0000000s
ReferenceId: 0x4C4F434C (source name:  "LOCL")
Last Successful Sync Time: 3/18/2024 5:18:04 PM
Source: Local CMOS Clock
Poll Interval: 6 (64s)
```

### Interpreting the Fields

#### Leap Indicator

```text
Leap Indicator: 0(no warning)
```

Indicates the status related to leap-second adjustments. The displayed value does not indicate any warning.

#### Stratum

```text
Stratum: 1
```

Represents the hierarchical level of the time source reported by the service.

#### Precision

```text
Precision: -23 (119.209ns per tick)
```

Represents the estimated precision of the system clock.

#### Root Delay

```text
Root Delay: 0.0000000s
```

Indicates the delay associated with communication with the time reference.

#### Root Dispersion

```text
Root Dispersion: 10.0000000s
```

Represents the estimated dispersion relative to the time reference.

#### ReferenceId

```text
ReferenceId: 0x4C4F434C (source name:  "LOCL")
```

Identifies the time reference reported by the service. In this output, `LOCL` corresponds to the local time reference.

#### Last Successful Sync Time

```text
Last Successful Sync Time: 3/18/2024 5:18:04 PM
```

Indicates the date and time recorded by the service as the last successful synchronization.

#### Source

```text
Source: Local CMOS Clock
```

Indicates that, in the displayed output, the reported time source was the local clock.

This is important because the activity configures `time.google.com`, but the output provided by the lab does not demonstrate that synchronization with Google's server actually occurred at that moment. The configured settings and the status reported by `w32tm` are distinct pieces of information.

#### Poll Interval

```text
Poll Interval: 6 (64s)
```

Indicates the interval used for synchronization queries.

## 10. Evidence

The required screenshot corresponds to Step 10 and shows the output of the following command:

```powershell
w32tm /query /status
```

**Caption to include before the screenshot:**

> Screenshot of Activity 12.02: the output of `w32tm /query /status` on Windows Server 2022, displaying the current Windows Time service status and parameters related to time synchronization.

[**View Evidence — Module 12 / Classes 45–46**](../evidencias.pdf)

## 11. Completion

After querying the service status, the windows used during the activity were closed.

## Key Concepts

- **NTP (Network Time Protocol):** A protocol used to synchronize clocks across networks.
- **W32Time:** The Windows service responsible for time synchronization functionality.
- **NTP Client:** A component used by Windows to query time sources.
- **NTP Server:** A feature that allows Windows to act as a time source for other clients.
- **w32tm:** A command-line tool used to configure and query the Windows Time service.
- **Stratum:** Indicates the hierarchical position of a time source within an NTP infrastructure.

## Activity Workflow

```text
Configure Group Policy
              ↓
Enable Windows NTP Server
              ↓
Enable Windows NTP Client
              ↓
Configure Windows NTP Client
              ↓
time.google.com,0x9
              ↓
Restart W32Time
              ↓
w32tm /query /status
              ↓
Query the service status
```

## Result

Windows Server 2022 was configured to enable the NTP client and server functionalities, with `time.google.com,0x9` specified as the NTP server. The Windows Time service was restarted, and its status was queried using `w32tm /query /status`.

However, the output provided by the lab reported `Local CMOS Clock` as the current time source. Therefore, it should not be interpreted as confirmation that synchronization with `time.google.com` actually occurred at that moment.

---

[Back to Classes 45–46](../README.md) · [Back to Module 12](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
