# Activity 7.05 — OneDrive Backup and Synchronization

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 25–26  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Configure OneDrive on a Windows Server 2022 client to back up and synchronize system folders with cloud storage.

---

## 1. Accessing Windows Server

The activity was performed on the Windows Server 2022 client through RDP.

After connecting, File Explorer was used to access:

```text
C:\curso
```

The following installer was available in this directory:

```text
OneDriveSetup
```

The installation was started using the required administrative permissions.

> Credentials used during the lab are not recorded in this README.

---

## 2. Configuring Internet Options

After installation, a Windows setting was configured to add the service used by OneDrive to the Trusted Sites zone.

In the Windows search menu, the following term was searched for:

```text
Internet Options
```

In the **Internet Properties** window, the following tab was opened:

```text
Security
```

Next, the following option was selected:

```text
Trusted Sites
```

Then, the following button was selected:

```text
Sites
```

The following address was added:

```text
https://odc.officeapps.live.com
```

The changes were then confirmed by selecting **Close** and **OK**.

---

## 3. Signing In to OneDrive

After the configuration, the **OneDrive** application was located using Windows Search.

The application was launched, and sign-in was completed using a Microsoft account.

After signing in, the OneDrive setup wizard was displayed.

---

## 4. Configuring the OneDrive Folder

In the setup wizard, the option for configuring the OneDrive folder was selected.

The process continued by selecting **Next**, keeping the configuration presented by the wizard.

---

## 5. Configuring Folder Backup

During the **Back up folders on this PC** step, the folders available for backup were displayed.

For this lab, only the following folder was selected:

```text
Desktop
```

Next, the following option was selected:

```text
Start backup
```

The wizard continued through the subsequent steps using **Next**.

---

## 6. Completing the Configuration

After proceeding through the wizard, the option related to the OneDrive mobile app was displayed.

The following option was selected:

```text
Later
```

This completed the step without configuring the mobile app.

---

## 7. Verifying Synchronization

To verify the configuration, the following option was selected:

```text
Open my OneDrive folder
```

File Explorer opened and displayed the synchronized OneDrive folder.

This step provided a visual check that OneDrive was configured on Windows Server and that the folder was available for synchronization with the cloud.

---

## Evidence

Evidence for this activity is included in the PDF for Module 7, Classes 25–26.

[View Evidence — Classes 25–26](../evidencias.pdf)

---

[Back to Classes 25–26](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
