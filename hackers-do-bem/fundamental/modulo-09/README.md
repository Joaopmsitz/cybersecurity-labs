# Module 09 — Digital Certificates and PKI

> **Program:** Hackers do Bem  
> **Stage:** Fundamental  
> **Module:** 09  
> **Status:** Completed

## Overview

This module covers Certificate Authorities (CAs), digital certificate issuance and management, web certificate verification, OCSP, certificate revocation, and Bitcoin wallet recovery using Electrum.

The activities use Windows Server 2022 and Kali Linux to explore public key infrastructure (PKI), certificate trust, revocation mechanisms, and cryptocurrency wallet security.

## Classes 33–34 — Certificate Authorities and Digital Certificates

| Activity | Topic | Description | View |
|---|---|---|---|
| 9.01 | Creating a Certificate Authority | Configure an Enterprise Root CA using Active Directory Certificate Services (AD CS). | [View](aula-33-34/atividade-9.01-criando-autoridade-certificadora/README.md) |
| 9.02 | Issuing Digital Certificates | Create and publish a certificate template and configure auto-enrollment through Group Policy. | [View](aula-33-34/atividade-9.02-emitindo-certificados/README.md) |
| 9.03 | Examining a Digital Certificate | Inspect an X.509 certificate, its properties, public key, validity, and certification path. | [View](aula-33-34/atividade-9.03-conhecendo-certificado-digital/README.md) |
| 9.04 | Evaluating Web Certificates | Examine an HTTPS certificate, its issuer, fingerprints, certificate fields, and PEM representation. | [View](aula-33-34/atividade-9.04-avaliando-certificados-web/README.md) |
| 9.05 | Creating Self-Signed Certificates | Generate an RSA private key, create a CSR, and issue a self-signed X.509 certificate with OpenSSL. | [View](aula-33-34/atividade-9.05-certificado-autoassinado-kali/README.md) |

**Evidence:** [View PDF — Classes 33–34](aula-33-34/evidencias.pdf)

## Classes 35–36 — Certificate Revocation and Bitcoin Wallets

| Activity | Topic | Description | View |
|---|---|---|---|
| 9.06 | Revoking a Digital Certificate | Revoke a previously issued certificate using the Certification Authority console. | [View](aula-35-36/atividade-9.06-revogando-certificado-windows-server/README.md) |
| 9.07 | Canceling Certificate Revocation | Use the Certification Authority console to cancel a certificate's revocation when permitted. | [View](aula-35-36/atividade-9.07-cancelar-revogacao-windows-server/README.md) |
| 9.08 | Verifying Web Certificates with OCSP | Inspect TLS certificate chains and OCSP stapling responses using OpenSSL. | [View](aula-35-36/atividade-9.08-verificando-certificados-web-ocsp-kali/README.md) |
| 9.09 | Creating a Bitcoin Wallet with Electrum | Create a standard Bitcoin wallet and review its information while protecting the seed phrase. | [View](aula-35-36/atividade-9.09-criando-carteira-bitcoin-electrum/README.md) |
| 9.10 | Recovering a Bitcoin Wallet | Restore a wallet using its seed phrase and create an on-chain payment request with a QR code. | [View](aula-35-36/atividade-9.10-recuperando-carteira-bitcoin-electrum/README.md) |

**Evidence:** [View PDF — Classes 35–36](aula-35-36/evidencias.pdf)

## Key Skills Practiced

- Deploying and managing an Enterprise Root CA with AD CS.
- Creating certificate templates and configuring auto-enrollment through Group Policy.
- Inspecting X.509 certificates, public keys, validity periods, fingerprints, and certification paths.
- Creating self-signed certificates with OpenSSL.
- Revoking and managing certificate status.
- Examining TLS certificate chains and OCSP responses.
- Creating and recovering Bitcoin wallets using Electrum.
- Generating payment requests and QR codes while protecting sensitive wallet information.

> **Security note:** Protect CA private keys and cryptocurrency seed phrases. Never publish private keys, seed phrases, passwords, or other sensitive credentials in a public repository. Certificate revocation and OCSP results should also be interpreted according to the status information and timestamps available at the time of verification.

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Repository](../../../README.md)
