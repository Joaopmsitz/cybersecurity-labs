# Activity 10.08 — Exploring a UEFI/BIOS Through Simulation

## Objective

Explore a simulated UEFI/BIOS interface provided by Lenovo, identifying system information and key settings related to hardware, security, and boot configuration.

## Environment

- **System:** Personal computer
- **Browser:** Mozilla Firefox
- **Resource:** Lenovo UEFI/BIOS Simulator
- **Simulated model:** Lenovo Slim Pro 9 16IRP8 (83C0)
- **Interface:** Graphics Interface Mode

## 1. Accessing the UEFI/BIOS Simulator

The activity was performed on a personal computer, as instructed by the lab, without using the AWS VM.

The following URL was accessed in the browser:

https://download.lenovo.com/bsco/index.html#/

Lenovo provides this resource to simulate the configuration interface of different devices.

## 2. Launching the Simulator

On the resource's home page, the following option was selected:

```text
Launch Simulator
```

Next, the following category was selected:

```text
Laptops
```

Then:

```text
Lenovo Laptops
```

## 3. Selecting the Device

From the list of available devices, the following model was selected:

```text
Lenovo Slim Pro 9 16IRP8 (83C0)
```

Next, the following option was chosen:

```text
Graphics Interface Mode
```

The simulated UEFI/BIOS interface then started.

## 4. Exploring the Information Section

On the initial screen of the simulated BIOS, the following section was reviewed:

```text
Information
```

This section displays information about the device, including:

- Product name
- BIOS version
- CPU
- System memory
- Secure Boot

This information makes it possible to check the device's basic specifications directly through the firmware interface.

## 5. Exploring the Configuration Section

In the left-hand menu, the following section was selected:

```text
Configuration
```

Settings related to the device's operation were reviewed, including:

- Time
- Date
- WLAN
- Graphics Device
- Intel(R) Virtualization Technology
- Always On USB
- Charge in Battery Mode
- System Performance Mode

The Configuration section brings together options related to the device's behavior and hardware features.

## 6. Exploring the Security Section

Next, the following section was selected:

```text
Security
```

The simulated UEFI/BIOS security settings were reviewed, including:

- Set Hard Disk Password
- Intel Platform Trust Technology
- Device Guard
- Secure Boot
- Reset to Setup Mode
- Restore Factory Keys

These options demonstrate how UEFI/BIOS can participate in mechanisms related to device protection, secure boot, and platform trust.

## 7. Exploring the Boot Section

In the left-hand menu, the following section was selected:

```text
Boot
```

Options related to the device's startup process were reviewed, including:

- USB Boot
- PXE Boot to LAN
- IPV4 PXE First
- EFI
- Windows Boot Manager
- EFI PXE Network

The Boot section allows users to review and configure different mechanisms and sources used during system startup.

### Evidence — Step 8

**Caption to include before the screenshot:**

> Screenshot of Activity 10.08: the Boot screen of the simulated UEFI/BIOS for the Lenovo Slim Pro 9 16IRP8 (83C0), displaying settings related to the boot process.

[View Evidence — Classes 39–40](../evidencias.pdf)

## 8. Exiting the Simulated UEFI/BIOS

After exploring the settings, the following menu option was accessed:

```text
Exit → Exit Discarding Changes
```

The following option was selected:

```text
Yes
```

The **Exit Discarding Changes** option closes the simulator without saving any changes made during the exploration.

Finally, the browser was closed.

## Key Concepts

- **UEFI:** Modern firmware responsible for initializing the computer and configuring hardware features.
- **BIOS:** Traditional firmware used to initialize and configure hardware.
- **Secure Boot:** A mechanism that helps verify authorized components during the boot process.
- **Boot:** The system startup process and selection of boot sources.
- **PXE:** A mechanism that enables network booting.

## Activity Workflow

```text
Access the simulator
      ↓
Launch Simulator
      ↓
Select Laptops
      ↓
Select the device model
      ↓
Explore Information
      ↓
Explore Configuration
      ↓
Explore Security
      ↓
Explore Boot
      ↓
Exit Discarding Changes
```

## Result

A simulated UEFI/BIOS interface was explored, identifying device information and hardware, security, and boot settings without needing to modify the computer's actual firmware.

---

[Back to Classes 39–40](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
