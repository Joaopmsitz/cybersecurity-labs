# Hackers do Bem — Fundamental | Module 01 — Classes 01–02

Documentation of the practical activities from Classes 01–02 of Module 01 of the Hackers do Bem Fundamental training stage.

These classes introduce file integrity verification, binary comparison, cryptographic hashing, classical encryption, and command-line task management through practical exercises in a Kali Linux environment.

## Class Overview

| Item | Details |
|---|---|
| Program | Hackers do Bem |
| Stage | Fundamental |
| Module | 01 |
| Classes | 01–02 |
| Activities | 5 |
| Main Topics | File Integrity, Binary Comparison, Hashing, Classical Cryptography, and Task Management |
| Primary Environment | Kali Linux |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 1.1 — Comparing Text Files to Detect Changes | File Integrity | Compare an original text file with a modified copy using `diff` to identify line-by-line changes. | [View Activity](./atividade-1.1-integridade-texto/README.md) |
| 1.2 — Comparing Binary File Integrity | Binary File Analysis | Compare identical and modified image files using `cmp` to identify byte-level differences. | [View Activity](./atividade-1.2-integridade-arquivos/README.md) |
| 1.3 — Verifying File Integrity with Hash Functions | Cryptographic Hashing | Calculate MD5 checksums with `md5sum` and compare digest values to identify file modifications. | [View Activity](./atividade-1.3-hash/README.md) |
| 1.4 — Classical Cryptography: ROT13 and Caesar Cipher | Classical Cryptography | Explore substitution ciphers through ROT13 and Caesar cipher encoding and decoding. | [View Activity](./atividade-1.4-criptografia/README.md) |
| 1.5 — Command-Line Task Management with Taskwarrior | Linux Administration | Use Taskwarrior to create, organize, list, and manage tasks from the Linux command line. | [View Activity](./atividade-1.5-taskwarrior/README.md) |

## Environment

The documented file integrity activities used Kali Linux and a working directory under `/home/aluno/Documentos`.

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| User Account | `aluno` |
| Working Directory | `/home/aluno/Documentos` |
| Terminal | Linux Terminal Emulator |
| File Editor | nano |
| Image Editor | KolourPaint |
| File Comparison | diff, cmp |
| Hash Utility | md5sum |
| Task Management | Taskwarrior |

Individual activity READMEs contain the specific commands, application settings, and environment details for each exercise.

## Tools and Technologies

| Category | Tools | Purpose |
|---|---|---|
| Text Comparison | `diff` | Identify line-by-line differences between text files. |
| Binary Comparison | `cmp` | Compare files byte by byte. |
| Cryptographic Hashing | `md5sum` | Generate MD5 digests for file comparison exercises. |
| File Editing | nano | Create and modify text files. |
| Image Editing | KolourPaint | Create and modify sample image files. |
| Classical Cryptography | ROT13, Caesar Cipher | Demonstrate substitution-based encoding and decoding. |
| Task Management | Taskwarrior | Create, organize, prioritize, and complete command-line tasks. |

## Learning Outcomes

- Understand the importance of file integrity verification.
- Compare text files and identify line-level modifications.
- Compare binary files and identify byte-level differences.
- Generate and compare cryptographic hash values.
- Understand the basic operation of classical substitution ciphers.
- Distinguish educational ciphers from modern cryptographic protection.
- Use Linux command-line tools for file administration.
- Organize and manage tasks using Taskwarrior.

## Evidence Requirements

The practical activities are documented in a single PDF for the Classes 01–02 group.

[View Class Evidence PDF](./evidencias.pdf)

The evidence file consolidates the supporting screenshots for the five activities.

## Technical Notes

- GNU `diff` compares text content line by line, while `cmp` performs byte-level comparison. The tools serve different purposes and should be selected according to the file format and investigation requirement.
- MD5 is demonstrated as a checksum algorithm in this exercise. It is not suitable when collision resistance is required, such as for digital signatures or security-sensitive integrity guarantees. SHA-256 is a better choice for modern security-oriented integrity verification.
- ROT13 and Caesar cipher are classical substitution techniques intended for educational purposes. They do not provide modern cryptographic security.
- Comparing files in a user-owned working directory generally does not require superuser privileges. Routine file operations should follow the principle of least privilege.

## References

- [GNU Diffutils Manual — diff and cmp](https://www.gnu.org/software/diffutils/manual/diffutils.html)
- [NIST — Secure Hash Standard](https://www.nist.gov/publications/secure-hash-standard)
- [RFC 6151 — Updated Security Considerations for MD5](https://www.rfc-editor.org/rfc/rfc6151)
- [Taskwarrior — Official Documentation](https://taskwarrior.org/docs/)
- [Taskwarrior — Command Reference](https://taskwarrior.org/docs/commands/)

---

[Back to Module 01](../README.md) · [Back to Fundamental](../../README.md) · [Back to Hackers do Bem](../../../README.md) · [Back to Cybersecurity Portfolio](../../../../README.md)
