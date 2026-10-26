# Module 08 — Cryptography and Data Protection

> **Program:** Hackers do Bem  
> **Stage:** Fundamental  
> **Module:** 08  
> **Status:** Completed

## Overview

This module covers steganography, Python code obfuscation, symmetric and asymmetric encryption, cryptographic hashes, and digital signatures. The activities use tools such as OpenSSL and Steghide in Kali Linux to demonstrate core cryptographic concepts and data protection techniques.

## Classes 29–30 — Steganography and Symmetric Encryption

| Activity | Topic | Description | View |
|---|---|---|---|
| 8.01 | Steganography on Kali Linux | Hide a text message inside a JPG image and extract the hidden file. | [View](aula-29-30/atividade-8.01-esteganografia-kali/README.md) |
| 8.02 | Python Code Obfuscation | Compile Python code into bytecode and examine the compiled file. | [View](aula-29-30/atividade-8.02-ofuscacao-python/README.md) |
| 8.03 | AES-256 Encryption and Decryption | Encrypt and recover an image file using AES-256-CTR with OpenSSL. | [View](aula-29-30/atividade-8.03-aes-256/README.md) |
| 8.04 | 3DES Encryption and Decryption | Encrypt and decrypt an image using Triple DES in CFB mode. | [View](aula-29-30/atividade-8.04-3des/README.md) |
| 8.05 | Blowfish Encryption and Decryption | Encrypt and recover an image using Blowfish in CFB mode. | [View](aula-29-30/atividade-8.05-blowfish/README.md) |

**Evidence:** [View PDF — Classes 29–30](aula-29-30/evidencias.pdf)

## Classes 31–32 — Hashing and Asymmetric Cryptography

| Activity | Topic | Description | View |
|---|---|---|---|
| 8.06 | MD5, RIPEMD-160, and BLAKE2 Hashes | Calculate and compare cryptographic digests using different hash algorithms. | [View](aula-31-32/atividade-8.06-hash-md5-ripemd160-blake2/README.md) |
| 8.07 | SHA-1, SHA-2, and SHA-3 Hashes | Compute and compare SHA-family digests with different output lengths. | [View](aula-31-32/atividade-8.07-hash-sha/README.md) |
| 8.08 | RSA-2048 for Confidentiality | Generate an RSA key pair and encrypt and decrypt a message. | [View](aula-31-32/atividade-8.08-rsa-2048-confidencialidade/README.md) |
| 8.09 | ECC-256 for Confidentiality | Generate ECC keys, derive a shared secret, and demonstrate symmetric encryption. | [View](aula-31-32/atividade-8.09-ecc-256-confidencialidade/README.md) |
| 8.10 | RSA-2048 Digital Signatures | Create and verify a digital signature, then test verification with modified content. | [View](aula-31-32/atividade-8.10-rsa-2048-assinatura-digital/README.md) |

**Evidence:** [View PDF — Classes 31–32](aula-31-32/evidencias.pdf)

## Key Skills Practiced

- Steganography and file extraction.
- Python bytecode compilation and code obfuscation concepts.
- Symmetric encryption using AES, 3DES, and Blowfish.
- Cryptographic hash calculation and comparison.
- Asymmetric cryptography using RSA and elliptic curves.
- Digital signature generation and verification.
- Understanding the limitations of legacy cryptographic algorithms and configurations.

> **Security note:** Some activities use legacy algorithms or demonstrate simplified cryptographic workflows for educational purposes. For real-world applications, prefer modern, authenticated encryption and current key derivation practices.

---

[Back to Fundamental](../README.md) · [Back to Hackers do Bem](../../README.md) · [Back to Repository](../../../README.md)
