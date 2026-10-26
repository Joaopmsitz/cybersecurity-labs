# Activity 9.01 — Creating a Certificate Authority on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 33–34  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Implement a Certificate Authority (CA) using Windows Server 2022 and the Active Directory Certificate Services (AD CS) role.

During this activity, an **Enterprise Root CA** was configured using:

- RSA with a 2048-bit key.
- SHA-256.
- A new private key.
- A CA certificate validity period of 10 years.
- The default certificate database location.

At the end of the activity, the Certificate Authority was available on the server under the name `aluno-DC01-CA`.

## Environment

- **Operating system:** Windows Server 2022
- **Service:** Active Directory Certificate Services (AD CS)
- **Role service:** Certification Authority
- **CA type:** Enterprise CA
- **Hierarchy:** Root CA
- **Cryptography:** RSA 2048-bit
- **Hash algorithm:** SHA-256
- **Configured validity period:** 10 years
- **Database location:** `C:\Windows\system32\CertLog`

> Credentials used to access the lab environment are not recorded in this README.

## 1. Opening Server Manager

After starting Windows Server 2022, Server Manager was opened using the Windows search field.

In the Server Manager interface, the following option was selected:

```text
Manage → Add Roles and Features
```

## 2. Starting the Role Installation

In the **Add Roles and Features Wizard**, the default options were retained, and the initial steps were completed by selecting **Next**.

Under **Server Roles**, the following role was located:

```text
Active Directory Certificate Services
```

The role was selected, and **Add Features** was chosen when prompted.

The wizard was then advanced to configure the role services.

## 3. Selecting the Certification Authority Service

Under **Role Services**, the following service was verified as selected:

```text
Certification Authority
```

The installation was started by selecting **Install**.

During the process, Server Manager displayed the following message:

```text
Installation started on DC01.aluno.hacker.com
```

The process was allowed to continue until the installation was complete.

## 4. Configuring Active Directory Certificate Services

After the role installation, the following option was selected:

```text
Configure Active Directory Certificate Services on the Destination server
```

In the **AD CS Configuration** window, the first step was completed, and the following service was selected:

```text
Certification Authority
```

## 5. Selecting the CA Type

Under the setup type, the following option was selected:

```text
Enterprise CA
```

This option integrates the Certificate Authority with the Active Directory environment.

Next, the following option was selected:

```text
Root CA
```

The configured authority therefore serves as a root CA within the lab's certificate hierarchy.

## 6. Creating the Private Key

Under private key configuration, the following option was selected:

```text
Create a new private key
```

The default cryptographic settings presented by the lab were retained:

```text
RSA 2048 bits
SHA-256
```

The generated private key is used by the Certificate Authority to sign the certificates it issues.

## 7. Configuring the CA Name

The common name suggested by the environment was retained:

```text
aluno-DC01-CA
```

The remaining fields were left at the default values presented by the wizard.

This name identifies the Certificate Authority that will subsequently be used to issue and manage certificates.

## 8. Setting the Validity Period

The default validity period presented by the wizard was five years.

It was changed to:

```text
10 years
```

This setting defines the validity period of the CA certificate.

## 9. Setting the Database Location

The default location for the CA database was retained:

```text
C:\Windows\system32\CertLog
```

This directory is used by the Certificate Services role to store information related to the Certificate Authority.

## 10. Applying the Configuration

After reviewing the configuration summary, the following option was selected:

```text
Configure
```

The process completed successfully, and the wizard displayed the following status:

```text
Configuration succeeded
```

The wizard windows were then closed.

## 11. Opening Certification Authority

In the Windows menu, the following folder was expanded:

```text
Windows Administrative Tools
```

The following tool was then selected:

```text
Certification Authority
```

The Certificate Authority management console opened.

## 12. Verifying the Certificate Authority

In the **Certification Authority (Local)** console, the following CA was found:

```text
aluno-DC01-CA
```

The presence of this authority confirms that the Certification Authority role was installed and configured on Windows Server 2022.

## Evidence — Step 16

The evidence requested for this activity corresponds to step 16, which requires a screenshot of the **Certification Authority (Local)** console displaying the authority:

```text
aluno-DC01-CA
```

Required caption before the screenshot:

> Screenshot for Activity 9.1: the Certification Authority (Local) console displaying the `aluno-DC01-CA` Certificate Authority configured on Windows Server 2022.

Evidence for this activity is included in the PDF for Module 9, Classes 33–34.

[View Evidence — Classes 33–34](../evidencias.pdf)

## Concepts Applied

### Certificate Authority

A Certificate Authority (CA) is responsible for issuing and signing digital certificates, establishing a trust relationship between the identity represented by a certificate and its public key.

### Active Directory Certificate Services

AD CS is the set of Windows Server services used to implement a public key infrastructure (PKI) in a Windows environment.

### Enterprise CA

An Enterprise CA is integrated with Active Directory, allowing domain resources to be used for certificate issuance, management, and distribution.

### Root CA

A Root CA sits at the top of a certificate hierarchy. Its key is used to sign its own certificate and, in hierarchical structures, can establish trust in subordinate CAs.

### Private Key

The CA's private key is one of the most sensitive components of the infrastructure. It is used to sign certificates issued by the authority and must be protected against unauthorized access.

## Result

An **Enterprise Root CA** was installed and configured on Windows Server 2022 using Active Directory Certificate Services.

The configuration used:

| Setting | Value |
|---|---|
| CA name | `aluno-DC01-CA` |
| Type | Enterprise CA |
| Hierarchy | Root CA |
| Key | RSA 2048 bits |
| Hash algorithm | SHA-256 |
| Validity period | 10 years |

The **Certification Authority (Local)** console confirmed the presence of the `aluno-DC01-CA` authority, completing the lab's Certificate Authority implementation.

---

[Back to Classes 33–34](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
