# Activity 9.09 — Creating a Bitcoin Wallet with Electrum

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 35–36  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Create a Bitcoin wallet using Electrum on Kali Linux, configure a standard wallet, and review its information after creation.

## Environment

- **Operating system:** Kali Linux
- **Application:** Electrum
- **Wallet type:** Standard wallet
- **Wallet name:** `default_wallet`

> The wallet's seed phrase is private information and must not be recorded, shared, or published. For security reasons, it has been omitted from this README.

## 1. Opening Electrum

Electrum was launched from the terminal:

```bash
electrum
```

The application opened to begin the wallet creation process.

## 2. Accepting the Terms

On the initial Electrum screen, the following option was selected:

```text
I Accept
```

Next, **Next** was selected to continue.

## 3. Setting the Wallet Name

On the wallet file selection screen, the default name was retained:

```text
default_wallet
```

Then, **Next** was selected.

## 4. Selecting the Wallet Type

On the wallet type configuration screen, the following option was selected:

```text
Standard wallet
```

Then, **Next** was selected.

## 5. Creating a New Seed

On the next screen, the following option was selected:

```text
Create a new seed
```

Then, **Next** was selected.

Electrum displayed an English seed phrase for the wallet.

This sequence can be used to recover the wallet if the local wallet file is lost. The seed phrase was written down for use in the next activity.

> **Important:** The seed phrase is equivalent to a credential that grants control over the wallet. It must never be included in GitHub repositories, READMEs, public screenshots, or shared with third parties.

## 6. Confirming the Seed

After generating the seed, Electrum requested that it be entered again to confirm that it had been recorded correctly.

The sequence was entered in the requested field, and the following option was selected:

```text
Next
```

The seed used in this activity is not reproduced in this document.

## 7. Configuring the Password

Electrum presented the option to set a password to protect the local wallet.

As requested in the lab, no additional password was configured.

Then, the following option was selected:

```text
Finish
```

The wallet was created.

## 8. Completing Wallet Creation

After the configuration was completed, Electrum loaded the wallet:

```text
default_wallet
```

The wallet was available for use in the application.

## 9. Update Notifications

Electrum displayed an option related to update notifications.

The following option was selected:

```text
No
```

This disabled these notifications during the lab.

## 10. Viewing Wallet Information

In Electrum's top menu, the following option was accessed:

```text
Wallet → Information
```

The information window displayed details associated with the newly created wallet.

This screen allows wallet information to be reviewed without exposing the seed phrase used during creation.

## Evidence — Step 10

Required caption before the screenshot:

> Screenshot for Activity 9.9: the Electrum **Wallet → Information** window, showing information about the wallet created during the activity.

Evidence for this activity is included in the PDF for Module 9, Classes 35–36.

> **Warning:** The seed phrase must not appear in the screenshot or be recorded in the repository. If any sensitive information is visible in the evidence, it must be concealed before publishing the material on GitHub.

## 11. Closing the Application

After capturing the evidence, Electrum was closed along with the terminal.

## Activity Workflow

| Stage | Result |
|---|---|
| Electrum | Application launched |
| Wallet | `default_wallet` created |
| Type | Standard wallet |
| Recovery | Seed phrase generated and stored privately |
| Verification | `Wallet → Information` |

## Result

A standard Bitcoin wallet was successfully created in Electrum, and its information was reviewed using **Wallet → Information**.

The seed phrase was kept out of the documentation to preserve wallet security.

---

[Back to Classes 35–36](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
