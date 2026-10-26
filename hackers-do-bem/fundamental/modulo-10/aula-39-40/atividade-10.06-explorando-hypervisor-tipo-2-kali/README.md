# Activity 10.06 — Exploring a Type 2 Hypervisor on Kali Linux

## Objective

Explore Oracle VM VirtualBox on Kali Linux by identifying its main settings and the features available in the hypervisor preferences.

VirtualBox is a **Type 2 hypervisor** because it runs on top of a host operating system and allows users to create and manage virtual machines.

## Environment

- **System:** Kali GNU/Linux
- **Hypervisor:** Oracle VM VirtualBox
- **Access:** RDP
- **VM IP address:** `192.168.98.40`

## 1. Opening VirtualBox

Kali Linux was accessed via RDP.

The following menu path was used from the top taskbar:

```text
Applications
→ Usual Applications
→ System
→ Oracle VM VirtualBox
```

After selecting the application, the main VirtualBox window opened.

## 2. Accessing Preferences

In the main VirtualBox window, the following menu option was selected:

```text
File → Preferences...
```

A new window displaying the general VirtualBox settings appeared.

## 3. Checking the Default Virtual Machine Folder

Under the **General** tab, the **Default Machine Folder** setting was checked.

The displayed path was:

```text
/home/aluno/VirtualBox VMs
```

This directory is used as the default storage location for virtual machines created with VirtualBox.

## 4. Checking the VRDP Authentication Library

Still within the general settings, the option related to the **VRDP Authentication Library** was examined.

VRDP (VirtualBox Remote Desktop Protocol) is used to enable remote desktop connections to VirtualBox virtual machines.

The default option displayed in the lab was:

```text
VBoxAuth
```

## 5. Exploring Input Settings

In the left-hand preferences panel, the following option was selected:

```text
Input
```

Under the tab for the VirtualBox Manager, the available VirtualBox management commands and their corresponding keyboard shortcuts were reviewed.

Next, the following option was selected:

```text
Virtual Machine
```

This section displayed commands and shortcuts related to virtual machine management.

## 6. Accessing Language Settings

In the left-hand preferences panel, the following option was selected:

```text
Language
```

The right-hand panel displayed the languages available for the VirtualBox interface.

The selected setting was:

```text
Default
```

In this mode, VirtualBox uses the language configured in the host operating system. Since the Kali Linux environment used in the lab was set to Portuguese, the VirtualBox interface was also displayed in Portuguese.

### Evidence — Step 6

**Caption to include before the screenshot:**

> Screenshot of Activity 10.06: the Oracle VM VirtualBox language settings screen, showing the available languages and the selected Default option.

[View Evidence — Classes 39–40](../evidencias.pdf)

## 7. Exploring Display Settings

After checking the language settings, the following option was selected:

```text
Display
```

The available settings for the graphical interface were reviewed, including:

- Maximum Guest Screen Size
- Scale Factor
- Extended Features
- Font Scaling

These options allow users to adjust aspects of virtual machine display and the graphical interface.

## 8. Closing Preferences

After exploring the settings, the following option was selected:

```text
OK
```

The **VirtualBox - Preferences** window closed.

VirtualBox remained open so the next activity could continue.

## Key Concepts

- **Type 2 Hypervisor:** Virtualization software that runs on top of a host operating system.
- **VirtualBox:** A platform used to create and manage virtual machines.
- **VRDP:** A protocol used by VirtualBox to provide remote access to virtual machines.
- **Preferences:** A collection of general settings used to configure VirtualBox.

## Activity Workflow

```text
Open VirtualBox
      ↓
Access Preferences
      ↓
Explore Settings
      ↓
Review Input
      ↓
Review Virtual Machine
      ↓
Review Language
      ↓
Review Display
      ↓
Close Preferences
```

## Result

The main VirtualBox preference settings were explored, including virtual machine storage, VRDP authentication, keyboard shortcuts, language, and display adjustments.

---

[Back to Classes 39–40](../) · [Back to Module 10](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
