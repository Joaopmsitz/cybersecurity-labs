# Activity 4.09 — TPM and USB

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 15–16  
> **Environment:** Kali Linux virtual machine  
> **Status:** Completed

## Objective

Check whether a **TPM (Trusted Platform Module)** is available in Kali Linux and identify USB devices available in the laboratory environment.

The activity also demonstrates how a virtualized environment may have limitations when accessing the physical machine's hardware.

## Environment

- Kali Linux running in a virtual machine
- Linux kernel
- TPM
- USB
- `journalctl`
- `usbview`

## Procedure

### 1. Check for TPM Availability

First, administrative access was obtained:

```bash
sudo -i
```

The kernel log was then queried for messages related to the TPM:

```bash
journalctl -k --grep=tpm
```

**Observed output:**

```text
fev 09 22:01:37 kali kernel: ima: No TPM chip found, activating TPM-bypass!
fev 09 22:01:37 kali systemd[1]: systemd 252.6-1 running in system mode (+PAM +AUDIT +SELINUX +APPARMOR +IMA +>
```

#### Interpretation

The message:

```text
No TPM chip found
```

indicates that the system did not find a TPM device available to the virtual machine.

As a consequence, the **IMA (Integrity Measurement Architecture)** activated a bypass mechanism to operate without a TPM.

This reflects a characteristic of the laboratory environment and does not, by itself, indicate that a system vulnerability exists.

### 2. Return to the Normal User

After completing the verification, the following command was used:

```bash
exit
```

This ended the elevated shell session and returned to the previous user context.

### 3. Check USB Devices

The graphical `usbview` utility was launched to inspect information about USB devices:

```bash
usbview
```

The following message appeared in the terminal:

```text
/sys/bus/usb/devices/ must be present, exiting...
```

Despite this initial message, the **USBView** graphical interface opened during the activity.

Because Kali Linux was running in a virtual machine, the physical computer's USB devices were not necessarily available to the guest operating system.

## Concepts Practiced

### TPM

The **Trusted Platform Module (TPM)** is a hardware-based security component used for operations involving cryptographic keys, boot integrity, and protected storage of sensitive information.

On compatible physical computers, the TPM can support operating system security features.

### IMA

The **Integrity Measurement Architecture (IMA)** is a Linux kernel mechanism used to measure and verify the integrity of files and system components.

In this laboratory, the log showed that IMA detected the absence of a TPM and activated the corresponding bypass mode.

### USBView

The `usbview` utility displays USB bus devices and related information.

In virtual machines, device availability depends on how hardware passthrough or USB sharing is configured between the host system and the virtual machine.

The terminal message alone does not establish that the physical USB hardware is unavailable in every circumstance; access depends on the guest environment and its configuration.

## Results

The kernel log indicated that **no TPM chip was available to Kali Linux in the virtualized environment**:

```text
ima: No TPM chip found, activating TPM-bypass!
```

The `usbview` utility was also executed to inspect the USB bus. The activity demonstrated a common limitation of virtualized environments: the guest operating system may not have direct access to the physical computer's hardware.

These observations apply to the laboratory environment and do not necessarily describe the capabilities of the physical host.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 15–16.

**Recorded screenshot:** Step 5 — running `usbview` and viewing its interface in the laboratory environment.

[View Evidence — Classes 15–16](../evidencias.pdf)

---

[Back to Classes 15–16](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
