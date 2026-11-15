# Activity 9.1 - Preparing a Forensic Toolkit

## Overview

This activity prepares a portable forensic workstation using Debian Linux and an external storage device.

The objective is to create bootable installation media and install forensic tools on a separate external device.

## Objectives

- Download the Debian netinst image.
- Create bootable USB installation media.
- Install Debian on a separate external storage device.
- Install common disk and filesystem examination utilities.
- Prepare an offline toolkit for future forensic work.

## Required Equipment

| Device | Minimum Suggested Capacity | Purpose |
|---|---:|---|
| Bootable USB drive | 2 GB | Debian installer |
| External USB drive or HDD | 4 GB | Debian system and forensic tools |

The training instructions recommend using two separate external devices.

## Procedure

### 1. Download Debian

Download the Debian netinst image for the appropriate architecture:

- [Debian - Network Installation](https://www.debian.org/distrib/netinst)

The course uses the `amd64` architecture for typical 64-bit PCs.

### 2. Create the Bootable USB

Download Rufus:

- [Rufus - Official Website](https://rufus.ie/)

In Rufus:

1. Connect the smaller USB drive.
2. Select the USB device.
3. Select the Debian ISO image.
4. Apply the compatibility option described in the course.
5. Start the writing process.
6. Confirm formatting only after verifying that the selected device is the intended boot USB.

The formatting process erases the selected USB drive.

### 3. Install Debian on the Separate External Device

Boot the computer from the prepared USB installer.

During installation, carefully select the larger external drive as the target for Debian.

Do not select the computer's internal system disk.

### 4. Install The Sleuth Kit

After booting into the external Debian environment, update package information:

```bash
apt-get update
```

Install The Sleuth Kit:

```bash
apt-get install sleuthkit
```

### 5. Install Additional Forensic Utilities

Foremost:

```bash
apt-get install foremost
```

Magic Rescue:

```bash
apt-get install magicrescue
```

Hexedit:

```bash
apt-get install hexedit
```

Hwinfo:

```bash
apt-get install hwinfo
```

GIMP:

```bash
apt-get install gimp
```

Search for additional forensic packages:

```bash
apt-cache search forensics
```

## Expected Result

A separate external Debian environment is prepared with The Sleuth Kit and additional forensic tools.

The environment can be used to perform later acquisition and analysis tasks without relying on the primary operating system installation.

## Evidence

No screenshot is required for Activity 9.1 in the course's final evidence PDF.

## Important Safety Notes

- This activity must be performed on the student's physical workstation.
- Do not perform this activity inside the course virtual machine.
- Verify the selected USB and installation target before formatting or installing Debian.
- Installing Debian on the wrong disk may erase the existing operating system and personal data.
- Back up important data before preparing any physical storage device.

## References

- [Debian - Network Installation](https://www.debian.org/CD/netinst/)
- [Rufus - Official Website](https://rufus.ie/)
- [The Sleuth Kit](https://github.com/sleuthkit/sleuthkit)

## Navigation

- [Class 09](../README.md)
- [Module 02](../../README.md)
- [Next Activity - 9.2](../atividade-9.2-coleta-evidencias-fisicas/README.md)
