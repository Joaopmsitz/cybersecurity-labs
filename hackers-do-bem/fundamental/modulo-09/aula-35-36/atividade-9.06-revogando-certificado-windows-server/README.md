# Activity 9.06 — Revoking a Certificate on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 35–36  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Revoke a digital certificate previously issued by the Windows Server 2022 Certificate Authority using the **Certification Authority** console.

The previous activities involving CA creation and certificate issuance were considered prerequisites for this exercise.

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

## 3. Viewing Issued Certificates

In the left pane of the window, the following authority was expanded:

```text
aluno-DC01-CA
```

The following folder was then selected:

```text
Issued Certificates
```

This section displays certificates issued by the Certificate Authority.

## 4. Selecting the Certificate

In the right pane, the first certificate in the list was selected.

The certificate was right-clicked, and the following options were accessed:

```text
All Tasks → Revoke Certificate
```

## 5. Selecting the Revocation Reason

In the revocation window, the following reason was selected:

```text
Certificate Hold
```

This option represents the temporary suspension of a certificate.

The operation was confirmed by selecting:

```text
Yes
```

The Certificate Authority then processed the certificate's revocation status.

## 6. Verifying the Result

After the operation, the following folder was selected again:

```text
Issued Certificates
```

According to the lab observations, the revoked certificate no longer appeared in this list, indicating that the Certificate Authority had processed the operation.

## Evidence — Step 6

Required caption before the screenshot:

> Screenshot for Activity 9.6: the Issued Certificates folder after the certificate revocation operation, showing the change in the list of issued certificates.

Evidence for this activity is included in the PDF for Module 9, Classes 35–36.

[View Evidence — Classes 35–36](../evidencias.pdf)

## Activity Workflow

| Stage | Result |
|---|---|
| Location | `Issued Certificates` |
| Action | `Revoke Certificate` |
| Reason | `Certificate Hold` |
| Result | Certificate status changed |

## Result

The certificate previously issued by `aluno-DC01-CA` was processed for revocation using the **Certification Authority** console.

---

[Back to Classes 35–36](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
