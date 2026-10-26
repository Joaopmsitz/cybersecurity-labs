# Activity 9.03 — Examining the Digital Certificate Obtained on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 33–34  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Access and analyze a digital certificate issued by the Certificate Authority configured in the previous activities.

This activity was performed on a Windows Server 2022 client. First, connectivity with the CA server was checked. The `aluno-DC01-CA` certificate installed in **Trusted Root Certification Authorities** was then examined.

The following information was inspected:

- Certificate version.
- Signature algorithm.
- Signature hash algorithm.
- Validity period.
- Public key.
- Key usage.
- Certification path.
- Certificate purposes.
- Information related to OCSP.

## Environment

- **Operating system:** Windows Server 2022
- **Client:** Windows Server 2022
- **Certificate Authority:** `aluno-DC01-CA`
- **Domain:** `aluno.hacker.com`
- **Certificate store:** Trusted Root Certification Authorities
- **Certificate analyzed:** `aluno-DC01-CA`

> Credentials used to access the lab environment are not recorded in this README.

## 1. Testing Connectivity to the Server

First, Command Prompt was opened on the Windows Server 2022 client.

Connectivity to the Certificate Authority server was tested using:

```cmd
ping 192.168.98.20
```

The output was:

```text
C:\Users\nome1>ping 192.168.98.20

Pinging 192.168.98.20 with 32 bytes of data:
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time=1ms TTL=128
```

The replies demonstrate that the client was able to communicate with the server.

## 2. Accessing Certificate Management

After the connectivity test, Command Prompt was closed.

The following term was entered in the Windows search field:

```text
Manage user certificates
```

The user certificate management console was then opened:

```text
certmgr
```

## 3. Locating the CA Certificate

In the certificate console, the following path was accessed:

```text
Trusted Root Certification Authorities
└── Certificates
```

The following certificate was located in this section:

```text
aluno-DC01-CA
```

The certificate identified the Certificate Authority itself as the issuer:

```text
Issued By: aluno-DC01-CA
```

This is expected for a Root CA because its root certificate is self-signed.

## 4. Opening the Certificate

The `aluno-DC01-CA` certificate was opened to view its properties.

The properties window contains several tabs that allow the certificate's information and extensions to be examined.

## 5. Examining the General Tab

The certificate's general information was reviewed under the **General** tab.

This section allows the following details to be checked, among others:

- To whom the certificate was issued.
- Who issued the certificate.
- The validity period.
- The certificate's trust status.
- The intended use of the key.

Reviewing this tab helps identify the relationship between the certificate installed on the client and the Certificate Authority responsible for issuing it.

## 6. Accessing the Certificate Details

Next, the following tab was selected:

```text
Details
```

This section displays the individual fields of the digital certificate.

The available fields include:

```text
Version
Signature algorithm
Signature hash algorithm
Valid to
Public Key
Key Usage
```

These fields allow the certificate's structure and cryptographic characteristics to be examined.

## 7. Examining the Main Fields

### Version

Indicates the version of the certificate standard being used.

Digital certificates based on X.509 use this field to identify the version of the certificate structure.

### Signature Algorithm

Identifies the algorithm used to generate the certificate's digital signature.

The signature allows the integrity of the certificate and its association with the signing authority to be verified.

### Signature Hash Algorithm

Indicates the hash algorithm used as part of the signing process.

The hash function transforms the certificate data into a digest, which is then used in the signature process.

### Valid To

Indicates the end of the certificate's validity period.

A certificate has a defined validity period and should not be considered valid for its intended purposes after that period expires.

### Public Key

Displays the public key associated with the certificate.

The public key can be distributed and used by third parties for cryptographic operations or signature verification, depending on the certificate's intended purpose.

### Key Usage

Defines the permitted cryptographic uses of the key according to the extensions present in the certificate.

## 8. Examining the Certification Path

After reviewing the **Details** tab, the following section was accessed:

```text
Certification Path
```

This section displays the trust hierarchy associated with the certificate.

Because the analyzed certificate belongs to the lab's root CA, it appears associated with the following authority:

```text
aluno-DC01-CA
```

The certification path is important for understanding how the system establishes trust between certificates and Certificate Authorities.

## 9. Examining Certificate Properties and Purposes

The certificate was right-clicked, and the following option was selected:

```text
Properties
```

Under the **General** tab, the following section was examined:

```text
Certificate purposes
```

This area identifies the purposes for which the certificate can be used.

The following tab was also inspected:

```text
OCSP
```

OCSP (**Online Certificate Status Protocol**) is used in certificate infrastructures to obtain certificate status information, including revocation status.

## Evidence — Step 10

The evidence requested for this activity corresponds to step 10 of the overall procedure, with the certificate's **Details** tab open.

Required caption before the screenshot:

> Screenshot for Activity 9.3: the Details tab of the `aluno-DC01-CA` certificate, displaying the version, signature algorithm, signature hash algorithm, validity, public key, and key usage fields.

The main fields expected on the screen are:

```text
Version
Signature algorithm
Signature hash algorithm
Valid to
Public Key
Key Usage
```

Evidence for this activity is included in the PDF for Module 9, Classes 33–34.

[View Evidence — Classes 33–34](../evidencias.pdf)

## Concepts Applied

### Digital Certificate

A digital certificate associates an identity with a public key and contains information that enables its use within a trust infrastructure.

### X.509

The analyzed certificate follows the structure defined by the X.509 standard, which specifies fields such as issuer, subject, validity, public key, signature, and extensions.

### Public Key

The public key is stored in the certificate and can be made available to other entities. Its use depends on the purpose defined in the certificate.

### Digital Signature

The CA's signature allows the certificate's integrity and its relationship with the signing authority to be verified.

### Certification Path

The certification path represents the chain of trust between the analyzed certificate and a trusted Certificate Authority.

### OCSP

OCSP is a protocol used to query the status of digital certificates, particularly to obtain revocation-related information.

## Analysis Workflow

```text
Windows Server 2022 Client
            │
            ▼
     Connectivity Test
            │
            ▼
   Manage user certificates
            │
            ▼
Trusted Root Certification Authorities
            │
            ▼
       aluno-DC01-CA
            │
            ├── General
            │
            ├── Details
            │
            ├── Certification Path
            │
            └── Certificate purposes / OCSP
```

## Result

The Certificate Authority certificate was located on the Windows Server 2022 client:

```text
aluno-DC01-CA
```

The analysis identified the main components of an X.509 digital certificate, including signature information, hash algorithm, validity, public key, and key usage.

The certification path was also examined, along with the **Certificate purposes** section and the OCSP reference in the certificate properties.

---

[Back to Classes 33–34](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
