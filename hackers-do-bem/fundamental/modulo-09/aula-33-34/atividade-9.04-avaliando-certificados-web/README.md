# Activity 9.04 — Evaluating Web Certificates on Windows Server 2022

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 33–34  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Analyze a digital certificate used by a website and examine its main security and identification properties.

During this activity, `https://www.google.com/` was accessed using Microsoft Edge. The certificate presented by the HTTPS connection was examined, then exported and opened in Notepad to inspect its structure in PEM format.

The following information was examined:

- Entity to which the certificate was issued.
- Issuing Certificate Authority.
- Validity period.
- Fingerprints.
- Certificate hierarchy.
- Certificate fields.
- PEM representation.

## Environment

- **Operating system:** Windows Server 2022
- **Browser:** Microsoft Edge
- **Protocol analyzed:** HTTPS
- **Website:** `https://www.google.com/`
- **Format examined after export:** PEM

## 1. Accessing the Website

Microsoft Edge was opened on Windows Server 2022.

The following website was accessed in the browser:

```text
https://www.google.com/
```

The website loaded over an HTTPS connection.

## 2. Verifying the Secure Connection

The security icon associated with the connection was selected in the browser's address bar.

The following indication was displayed:

```text
Connection is secure
```

This indicates that the browser established an HTTPS connection and performed the corresponding checks on the certificate presented by the server.

## 3. Accessing the Certificate

From the secure connection information, the certificate-related icon was selected.

The digital certificate information used by the website was displayed.

## 4. Examining the General Information

The following certificate details were observed in the **General** section:

```text
Issued To
Issued By
Validity Period
Fingerprints
```

### Issued To

Identifies the entity or names associated with the certificate.

### Issued By

Identifies the Certificate Authority responsible for issuing the certificate.

### Validity Period

Displays the period during which the certificate is considered valid.

### Fingerprints

Fingerprints are identifiers derived from certificate content using hash functions. They can be used to compare or identify a specific certificate.

## 5. Examining the Certificate Details

The following sections were examined in the certificate details view:

```text
Certificate Hierarchy
Certificate Fields
```

**Certificate Hierarchy** displays the chain of trust used to validate the certificate.

**Certificate Fields** displays the fields that make up the digital certificate structure, including information about the subject, issuer, validity, public key, signature, and extensions.

## 6. Exporting the Certificate

The certificate was exported to the computer using the export option provided by the browser.

The file was saved in the following directory:

```text
Downloads
```

This step made it possible to examine the certificate contents outside the browser's graphical interface.

## 7. Opening the Certificate in Notepad

After exporting the certificate, Notepad was opened.

From the menu, the following option was selected:

```text
File → Open
```

The following folder was accessed:

```text
Downloads
```

The file filter was changed to:

```text
All files
```

This made it possible to locate and open the exported certificate file.

## 8. PEM Structure

When the exported certificate was opened in Notepad, its representation in PEM (**Privacy-Enhanced Mail**) format became visible.

A PEM-encoded certificate typically has a structure similar to the following:

```text
-----BEGIN CERTIFICATE-----
[Base64-encoded content]
-----END CERTIFICATE-----
```

The content between the markers is the Base64 representation of the certificate.

Base64 encoding is not encryption. It represents binary data as text, facilitating storage and transport in environments that work with textual content.

## Evidence — Step 14

The evidence requested for this activity corresponds to step 14, showing the exported certificate open in Notepad with its PEM structure visible.

Required caption before the screenshot:

> Screenshot for Activity 9.4: the exported web digital certificate opened in Notepad, displaying its PEM structure with the `BEGIN CERTIFICATE` and `END CERTIFICATE` markers.

The screenshot should clearly show the structure of the exported certificate.

Evidence for this activity is included in the PDF for Module 9, Classes 33–34.

[View Evidence — Classes 33–34](../evidencias.pdf)

## Concepts Applied

### HTTPS

HTTPS uses TLS to protect communication between a client and a server. The digital certificate presented by the server participates in server identity authentication and in establishing a secure connection.

### X.509 Certificate

Certificates used in TLS connections generally follow the X.509 standard and contain information about the subject, issuer, validity, public key, signature, and extensions.

### Certificate Authority

A Certificate Authority signs digital certificates to establish a chain of trust.

The browser uses the information contained in the certificate and its certification chain to perform the required validation checks.

### Fingerprint

A fingerprint is a cryptographic digest of a certificate. It can be used to identify and compare certificates.

### PEM

PEM represents binary cryptographic data as text using Base64 encoding and delimiters.

Example:

```text
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
```

The Base64 content can subsequently be decoded back into its original binary representation.

## Activity Workflow

```text
Microsoft Edge
      │
      ▼
https://www.google.com/
      │
      ▼
HTTPS Connection
      │
      ▼
Server Certificate
      │
      ├── Issued To
      ├── Issued By
      ├── Validity Period
      ├── Fingerprints
      ├── Certificate Hierarchy
      └── Certificate Fields
              │
              ▼
            Export
              │
              ▼
           Downloads
              │
              ▼
            Notepad
              │
              ▼
         PEM Structure
```

## Result

A digital certificate used in an HTTPS connection was examined, allowing its general information, issuing authority, validity period, fingerprints, hierarchy, and certificate fields to be reviewed.

After export, the certificate was opened in Notepad, and its PEM representation, containing the `BEGIN CERTIFICATE` and `END CERTIFICATE` delimiters, was identified.

The activity demonstrated the relationship between digital certificates, server authentication in HTTPS connections, and the structure used to represent certificates in a text-based format.

---

[Back to Classes 33–34](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
