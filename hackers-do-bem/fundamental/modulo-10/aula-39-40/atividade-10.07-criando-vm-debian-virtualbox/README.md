# Activity 10.07 — Creating a VM on a Type 2 Hypervisor on Kali Linux

## Objective

Create a virtual machine using Oracle VM VirtualBox on Kali Linux, configuring an installation based on the Debian 12.5.0 AMD64 Netinst image.

This activity demonstrates the process of creating a VM on a Type 2 hypervisor, including ISO image selection, user configuration, memory allocation, and storage configuration.

## Environment

- **Host operating system:** Kali GNU/Linux
- **Hypervisor:** Oracle VM VirtualBox
- **Guest operating system:** Debian Netinst
- **ISO image:** `debian-12.5.0-amd64-netinst.iso`
- **Configured memory:** 512 MB
- **Configured disk:** 10 GB
- **VM name:** `DebianNetinst`

## 1. Starting the Virtual Machine Creation Process

With VirtualBox still open from the previous activity, the window displaying the following message was closed:

```text
Could not enumerate USB devices...
```

Next, the following menu option was selected from the VirtualBox menu bar:

```text
Machine → New
```

This opened the wizard for creating a new virtual machine.

## 2. Defining the VM Name

The following name was entered in the virtual machine identification field:

```text
DebianNetinst
```

This is the name VirtualBox will use to identify the virtual machine.

## 3. Selecting the ISO Image

In the **ISO Image** field, the following option was selected:

```text
Other
```

In the file selection window, the following locations were accessed:

```text
Other Locations
→ Computer
→ curso
```

The following image was located:

```text
debian-12.5.0-amd64-netinst.iso
```

The image was selected by double-clicking it.

## 4. Proceeding Through the Wizard

After selecting the Debian ISO image, the following button was clicked:

```text
Next (N)
```

The wizard proceeded to the user configuration screen.

## 5. Configuring the User

In the **Username** field, the default name was changed to:

```text
DebianNetinst
```

The password provided by the lab was also reviewed.

After completing the configuration, the following button was clicked:

```text
Next (N)
```

The lab credentials are not reproduced here beyond what is necessary to document the configuration.

## 6. Configuring Memory

On the hardware configuration screen, the **Base Memory** value was set to:

```text
512 MB
```

The following button was then clicked:

```text
Next (N)
```

## 7. Configuring Storage

On the virtual disk configuration screen, the disk size was changed to:

```text
10 GB
```

The following button was then clicked:

```text
Next (N)
```

## 8. Completing the VM Creation Process

VirtualBox displayed a summary of the selected configuration.

After reviewing the information, the following button was clicked:

```text
Finish
```

The virtual machine was then created in VirtualBox.

### Evidence — Step 9

**Caption to include before the screenshot:**

> Screenshot of Activity 10.07: the newly created DebianNetinst virtual machine displayed in the left-hand pane of Oracle VM VirtualBox.

[View Evidence — Classes 39–40](../evidencias.pdf)

## 9. Verifying the Created Virtual Machine

After the wizard was completed, the following VM appeared in the left-hand pane of VirtualBox:

```text
DebianNetinst
```

The virtual machine was created with the settings specified in the wizard, including the Debian Netinst ISO image, 512 MB of memory, and 10 GB of storage.

The lab also states that the AWS VM environment does not have a virtualization driver available. Therefore, it is not necessary to start the DebianNetinst virtual machine in this environment.

If the VM is started in this environment, the following error may occur:

```text
Kernel driver not installed
```

The virtual machine creation process was completed successfully despite this limitation.

## 10. Closing the Activity

The DebianNetinst virtual machine was created and remained available in VirtualBox for a potential Debian installation.

Starting the virtual machine or installing the operating system was not required for this activity.

After completion, the windows were closed, the RDP connection was terminated, and the AWS VM session was stopped, as instructed by the lab.

## Key Concepts

- **Virtual machine (VM):** An isolated computing environment running on a hypervisor.
- **Netinst ISO:** A minimal Debian installation image used to start the installation process and obtain the required components.
- **Type 2 hypervisor:** Virtualization software that runs on top of a host operating system.
- **VirtualBox:** A hypervisor used to create and manage virtual machines.

## Activity Workflow

```text
Open VirtualBox
      ↓
Machine → New
      ↓
Set the name to DebianNetinst
      ↓
Select the ISO image
      ↓
Configure the user
      ↓
Allocate 512 MB RAM
      ↓
Configure a 10 GB disk
      ↓
Finish
      ↓
VM created
```

## Result

The `DebianNetinst` virtual machine was created using the Debian Netinst image, with 512 MB of memory and 10 GB of storage, and became available in the VirtualBox interface.

---

[Back to Classes 39–40](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
