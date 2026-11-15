# Hackers do Bem - Specialization | Module 03 - Class 01 (Course Lesson 11)

This class introduces practical computer forensic investigation techniques through timeline analysis, case reconstruction, password auditing, ZIP password recovery, and steganography.

The practical activities use The Sleuth Kit, Autopsy, John the Ripper, fcrackzip, and Steghide.

## Class Overview

| Item | Description |
|---|---|
| Program | Hackers do Bem |
| Track | Incident Response and Digital Forensics |
| Module | 03 - Computer Forensics |
| Class | 01 |
| Course Lesson | 11 |
| Main Topic | Computer Forensic Investigation |
| Main Technologies | The Sleuth Kit, Autopsy, John the Ripper, fcrackzip, Steghide |

## Practical Activities

| Activity | Topic | Description | Documentation |
|---|---|---|---|
| 11.1 | Timeline Analysis | Generate and inspect a chronological file activity timeline using mactime. | [View Activity](./atividade-11.1-linha-do-tempo-mactime/README.md) |
| 11.2 | Reconstruction of Events | Analyze the recovered `lucros.xls` spreadsheet in Autopsy and reconstruct the financial fraud scenario. | [View Activity](./atividade-11.2-reconstrucao-fatos-autopsy/README.md) |
| 11.3 | Password Auditing with John the Ripper | Audit the supplied Unix password hashes using a wordlist. | [View Activity](./atividade-11.3-john-the-ripper/README.md) |
| 11.4 | ZIP Password Recovery | Perform a controlled brute-force test against the supplied encrypted ZIP archive. | [View Activity](./atividade-11.4-senha-arquivo-zip-fcrackzip/README.md) |
| 11.5 | Steganography | Extract hidden information from a JPEG image using Steghide. | [View Activity](./atividade-11.5-esteganografia-steghide/README.md) |

## Environment

The activities use the forensic datasets and tools supplied by the training environment.

| Component | Purpose |
|---|---|
| The Sleuth Kit | Filesystem metadata examination and timeline generation |
| mactime | Chronological timeline creation |
| Autopsy | Digital forensic case analysis |
| John the Ripper | Password hash auditing |
| fcrackzip | ZIP password recovery |
| Steghide | Steganographic data extraction |

## Tools and Technologies

- The Sleuth Kit
- mactime
- Autopsy
- John the Ripper
- fcrackzip
- Steghide
- Linux
- Windows
- Digital forensics
- Timeline analysis
- Password auditing
- Steganography

## Learning Outcomes

- Generate forensic timelines from filesystem metadata.
- Interpret chronological file activity.
- Investigate recovered files using Autopsy.
- Correlate financial records and artifacts during case reconstruction.
- Audit Unix password hashes using John the Ripper.
- Understand brute-force ZIP password recovery.
- Extract hidden information from image files.
- Document forensic results and preserve evidence.

## Evidence

A single PDF contains the screenshots required for all five practical activities.

| Activity | Required Evidence | PDF Page |
|---|---|---|
| 11.1 | `mactime` execution and the contents of `otavio.timeline`, showing chronological activity from May 2010. | 1 |
| 11.2 | Autopsy view of the recovered `lucros.xls` spreadsheet, supporting the reconstruction of the fraudulent transactions and beneficiary accounts. | 2 |
| 11.3 | John the Ripper command and output showing the recovered password `harrypotter`. | 3 |
| 11.4 | fcrackzip execution showing the recovered ZIP password `anarc`. | 4 |
| 11.5 | Steghide extraction from `fun.jpg` and the contents of the recovered `festa.txt` file. | 5 |

- [View consolidated evidence - evidences.pdf](./evidences.pdf)

The PDF is stored at the class level and consolidates the five required screenshots.

## Technical Notes

- mactime reads a body file produced in The Sleuth Kit body-file format and sorts filesystem activity chronologically.
- Autopsy supports file analysis, timeline investigation, and examination of recovered evidence.
- John the Ripper supports wordlist-based password auditing and multiple hash formats.
- fcrackzip supports brute-force and dictionary-based ZIP password recovery.
- Steghide extracts embedded content from supported cover files, including JPEG images.
- Password recovery activities must be limited to the course-provided files and explicitly authorized forensic investigations.
- Extracted password material and financial evidence may contain sensitive information. Do not publish raw hashes, recovered credentials, or confidential case files.

## References

- [The Sleuth Kit - Body File Format](https://wiki.sleuthkit.org/Body-file/)
- [The Sleuth Kit - mactime](https://github.com/sleuthkit/sleuthkit/wiki/mactime)
- [Autopsy - Timeline Documentation](https://sleuthkit.org/autopsy/docs/user-docs/4.22.0/timeline_page.html)
- [Autopsy - Quick Start Guide](https://sleuthkit.org/autopsy/docs/user-docs/4.22.0/quick_start_guide.html)
- [John the Ripper - Official Documentation](https://www.openwall.com/john/doc/)
- [John the Ripper - Command-Line Options](https://www.openwall.com/john/doc/OPTIONS.shtml)
- [fcrackzip - Debian Manual](https://sources.debian.org/src/fcrackzip/1.0-8/fcrackzip.1)
- [Steghide - Manual](https://steghide.sourceforge.net/documentation/manual.pdf)

## Navigation

- [Module 03](../README.md)
- [Previous Module - 02](../../modulo-02/README.md)
- [Specialization Overview](../../README.md)
