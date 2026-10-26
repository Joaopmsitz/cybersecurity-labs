# Activity 10.01 — Memory Integrity and Maintenance in Windows Server 2022

## Objective

Explore the Memory Integrity, Core Isolation, and Security and Maintenance features in Windows Server 2022, while also reviewing the reliability history and automatic maintenance capabilities of the system.

## Environment

- **System:** Windows Server 2022
- **Features explored:** Windows Security and Security and Maintenance
- **Access:** RDP
- **Machine:** Windows Server 2022 (client)

The credentials used to access the lab are not included in this README.

## 1. Accessing Windows Server 2022

The Windows Server 2022 client was accessed via RDP.

The administrative user specified by the lab was used on the authentication screen.

## 2. Accessing Device Security

On the taskbar, the following search field was selected:

```text
Type here to search
```

The following term was searched for:

```text
Device security
```

The **Device security** feature was then opened.

## 3. Checking Core Isolation

In the Device security window, the following section was located:

```text
Core Isolation
```

Core Isolation uses hardware-based virtualization features to create an isolation layer for critical system components, particularly those associated with the kernel.

This mechanism helps reduce the attack surface and makes it more difficult for techniques targeting low-level operating system components to compromise them.

## 4. Accessing Core Isolation Details

The following link was selected to view the available settings:

```text
Core isolation details
```

## 5. Checking Memory Integrity

On the details page, the following option was located:

```text
Memory integrity
```

This feature is designed to protect system memory integrity by making unauthorized modifications to code running in protected Windows components more difficult.

## 6. Enabling Memory Integrity

The Memory integrity toggle was initially set to:

```text
Off
```

It was changed to:

```text
On
```

The feature was therefore enabled in the settings.

## 7. Restarting the Server

After the feature was enabled, Windows displayed a notification indicating that the system needed to be restarted.

The following options were selected from the taskbar:

```text
Windows → Shut down or sign out → Restart → Continue
```

The machine restarted, and the RDP connection was interrupted during the process.

## 8. Reconnecting After the Restart

After waiting for the period specified by the lab, the Windows Server 2022 machine was accessed again via RDP.

The status of Memory integrity was checked after reconnecting.

> The lab material notes that, because of how the virtual machine is managed in this environment, the feature may continue to appear as **Off** even after an attempt to enable it.

## 9. Accessing Security and Maintenance

The following term was searched for from the taskbar:

```text
Security and Maintenance
```

The feature was opened to explore the system's maintenance and reliability options.

## 10. Viewing the Reliability History

In the Security and Maintenance window, the following section was selected:

```text
Maintenance
```

After expanding the section, the following option was selected:

```text
View reliability history
```

Reliability Monitor provides a history of events related to system stability, including application failures, problems, and other relevant events.

## 11. Viewing Problem Reports

In the Reliability History window, the following option was selected:

```text
View all problem reports
```

This option allows users to review reports of problems recorded by the system, such as application failures and other events that may affect system reliability.

After reviewing the reports, **OK** was selected in the necessary windows to return to the previous screen.

## 12. Configuring Automatic Maintenance

Back in the **Maintenance** section, the following option was selected:

```text
Change Maintenance Settings
```

This setting allows users to adjust the Windows automatic maintenance schedule and define when these activities can run.

After reviewing the settings, the following option was selected:

```text
Cancel
```

This closed the settings without making any changes.

## 13. Starting Maintenance

In the **Maintenance** section, the following option was selected:

```text
Start maintenance
```

This option manually starts the maintenance activities available on the system.

The process may involve tasks related to system maintenance and health checks.

### Evidence — Step 13

Caption to include before the screenshot:

> Screenshot of Activity 10.01: the **Start maintenance** option in the Maintenance section of Windows Server 2022, demonstrating the option to manually start system maintenance.

[View Evidence — Classes 37–38](../evidencias.pdf)

## 14. Checking the Maintenance Status

After starting maintenance, the following notification was observed:

```text
Maintenance in progress
```

This notification indicates that the maintenance process has started.

After checking the status, the windows were closed.

## Activity Workflow

| Step | Result |
|---|---|
| Device Security | Explored Core Isolation and Memory Integrity |
| Memory Integrity | Attempted to enable the feature and restarted the system |
| Security and Maintenance | Explored the maintenance features |
| Start maintenance | Started the maintenance process |

## Result

The Core Isolation, Memory Integrity, and Security and Maintenance features in Windows Server 2022 were explored.

The system maintenance process was also started manually, and the **Maintenance in progress** status was verified.

---

[Back to Classes 37–38](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
