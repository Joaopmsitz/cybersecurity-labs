# Activity 9.07 — Unrevoking a Certificate on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 35–36  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Cancel the revocation of a previously revoked certificate in the Windows Server 2022 Certificate Authority, returning the certificate to the list of issued certificates.

## Environment

- **Operating system:** Windows Server 2022
- **Service:** Active Directory Certificate Services (AD CS)
- **Certificate Authority:** `aluno-DC01-CA`
- **Console:** Certification Authority

> Credentials used to access the lab environment are not recorded in this README.

## 1. Opening Server Manager

The Windows search field was opened, and the following term was searched for:

```text
Server Manager
```

Server Manager was then opened.

## 2. Accessing Certification Authority

In Server Manager, the following option was selected:

```text
Tools → Certification Authority
```

The Certificate Authority management console opened.

## 3. Accessing Revoked Certificates

In the left pane, the following authority was expanded:

```text
aluno-DC01-CA
```

The following folder was then selected:

```text
Revoked Certificates
```

This folder displays certificates that have been revoked by the Certificate Authority.

## 4. Viewing the Certificate

In the right pane, the certificate revoked in the previous activity was located.

The certificate was double-clicked to view the following tabs:

```text
General
Details
Path
```

After reviewing the information, **OK** was selected.

## 5. Viewing Attributes and Extensions

The certificate was right-clicked, and the following options were accessed:

```text
All Tasks → View Attributes/Extensions...
```

In the window that opened, the following tabs were examined:

```text
Attributes
Extensions
```

These sections display the attributes and extensions associated with the certificate.

After reviewing the information, **OK** was selected.

## 6. Canceling the Revocation

With the certificate selected, the context menu was opened, and the following option was accessed:

```text
All Tasks → Unrevoke Certificate
```

The **Unrevoke Certificate** option cancels the revocation recorded for the certificate.

## 7. Verifying Revoked Certificates

After the operation, the following folder was checked again:

```text
Revoked Certificates
```

The certificate no longer appeared in this list.

## 8. Accessing Issued Certificates

In the left pane of the console, the following folder was selected:

```text
Issued Certificates
```

## 9. Verifying the Certificate

In the **Issued Certificates** folder, the certificate whose revocation had been canceled was located again.

This demonstrates that the certificate returned to the list of issued certificates after the **Unrevoke Certificate** operation.

## Evidence — Step 9

Required caption before the screenshot:

> Screenshot for Activity 9.7: the certificate whose revocation was canceled, appearing again in the Issued Certificates folder of the Certificate Authority.

Evidence for this activity is included in the PDF for Module 9, Classes 35–36.

[View Evidence — Classes 35–36](../evidencias.pdf)

## Activity Workflow

| Stage | Result |
|---|---|
| Certificate | Located in `Revoked Certificates` |
| Action | `Unrevoke Certificate` |
| Verification | Removed from `Revoked Certificates` |
| Final result | Returned to `Issued Certificates` |

## Result

The certificate's revocation was successfully canceled, causing it to appear again in the `Issued Certificates` folder of `aluno-DC01-CA`.

---

[Back to Classes 35–36](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
