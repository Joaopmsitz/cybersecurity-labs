# Activity 10.02 — App and Browser Control in Windows Server 2022

## Objective

Explore the **App & browser control**, **Reputation-based protection**, and **Exploit Protection** features in Windows Security on Windows Server 2022, reviewing the main security settings designed to protect against malicious applications and exploitation techniques.

## Environment

- **System:** Windows Server 2022
- **Tool:** Windows Security
- **Features:** App & browser control, Reputation-based protection, and Exploit Protection
- **Access:** RDP
- **Machine:** Windows Server 2022 (client)

The credentials used to access the lab are not included in this README.

## 1. Accessing Windows Server 2022

The Windows Server 2022 client was accessed via RDP using the administrative credentials specified by the lab.

## 2. Accessing App & browser control

The following search field was selected from the taskbar:

```text
Type here to search
```

The following term was searched for:

```text
App & browser control
```

The feature was then opened.

## 3. Checking Reputation-based protection

In the **App & browser control** window, the following section was located:

```text
Reputation-based protection
```

In the initial state observed during the activity, the feature was disabled and displayed the following option:

```text
Turn on
```

Reputation-based protection uses information about files, applications, and their sources to help identify potentially malicious content.

## 4. Accessing Reputation-based Protection Settings

The following link was selected to view the available settings:

```text
Reputation-based protection settings
```

## 5. Checking Check apps and files

On the settings page, the following option was located:

```text
Check apps and files
```

This setting allows applications and files to be checked against reputation information, helping identify potentially dangerous content before it is executed or opened.

## 6. Enabling Potentially unwanted app blocking

The following option was located:

```text
Potentially unwanted app blocking
```

The feature was initially set to:

```text
Off
```

It was changed to:

```text
On
```

This mechanism helps block potentially unwanted applications (PUAs), which may exhibit undesirable behavior even when they are not necessarily classified as traditional malware.

## 7. Returning to the Previous Page

The back button in the upper-left corner was used to return to the main **App & browser control** page.

## 8. Verifying Reputation-based Protection

After the previous change, the status of **Reputation-based protection** was checked.

The feature was now displayed as enabled.

## 9. Accessing Exploit Protection

On the **App & browser control** page, the **Exploit protection** section was located.

Exploit Protection provides mitigation mechanisms designed to make it more difficult to exploit vulnerabilities in applications and the operating system itself.

The following link was selected:

```text
Exploit protection settings
```

## 10. Reviewing System Protections

On the Exploit protection page, the following tab was selected:

```text
System settings
```

Several system protections that were enabled by default were observed.

### Control Flow Guard (CFG)

Control Flow Guard helps protect applications against techniques that attempt to alter or redirect a program's normal execution flow.

### Data Execution Prevention (DEP)

Data Execution Prevention helps prevent code from executing in certain memory regions designated for data, reducing the impact of some exploitation techniques.

### Force randomization for images (Mandatory ASLR)

This setting uses Address Space Layout Randomization (ASLR) to make the memory addresses used by program modules more difficult to predict.

### Randomize memory allocations (Bottom-up ASLR)

This setting randomizes memory allocations, making it more difficult for an attacker to rely on predictable memory addresses during an exploit.

### High-entropy ASLR

This setting increases the amount of randomness used in memory address allocation, making addresses more difficult to predict in supported environments.

### Validate exception chains (SEHOP)

Structured Exception Handling Overwrite Protection (SEHOP) helps validate exception-handling chains, making certain exploitation techniques that rely on corruption of these structures more difficult.

### Validate heap integrity

This setting performs checks related to the integrity of heap structures, helping detect conditions associated with memory corruption.

### Evidence — Step 10

Caption to include before the screenshot:

> Screenshot of Activity 10.02: the **Exploit protection settings** screen, on the **System settings** tab, showing the settings designed to mitigate exploitation techniques in Windows Server 2022.

[View Evidence — Classes 37–38](../evidencias.pdf)

## 11. Closing the Activity

After reviewing the settings, all windows were closed.

## Activity Workflow

| Step | Result |
|---|---|
| App & browser control | Feature explored |
| Reputation-based protection | Settings reviewed |
| Potentially unwanted app blocking (PUA Blocking) | Enabled |
| Exploit Protection | System protection settings reviewed |

## Result

The application and browser protection mechanisms in Windows Security were explored.

The main Exploit Protection mitigations were also reviewed, including CFG, DEP, ASLR, SEHOP, and heap integrity validation.

---

[Back to Classes 37–38](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
