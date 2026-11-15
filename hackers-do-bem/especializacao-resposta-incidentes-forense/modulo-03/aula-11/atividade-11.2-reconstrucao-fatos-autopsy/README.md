# Activity 11.2 - Reconstruction of Events with Autopsy

## Overview

This activity uses Autopsy to examine recovered digital evidence and reconstruct the facts of a financial fraud investigation.

The practical exercise focuses on the recovered `lucros.xls` spreadsheet and the transactions described in the training case.

## Objectives

- Review the forensic case in Autopsy.
- Locate and examine the recovered `lucros.xls` spreadsheet.
- Identify transaction records relevant to the investigation.
- Correlate the spreadsheet contents with the case narrative.
- Document the evidence supporting the reconstruction of events.

## Environment

| Component | Description |
|---|---|
| Forensic Platform | Autopsy |
| Operating System | Windows |
| Main Artifact | `lucros.xls` |
| Investigation Type | Financial fraud case reconstruction |

## Procedure

### 1. Open the Forensic Case

Start Autopsy on the Windows laboratory environment and open the case supplied by the training activity.

Review the case data source and the artifacts identified during processing.

### 2. Locate the Recovered Spreadsheet

Locate the recovered file:

```text
lucros.xls
```

Open the artifact in Autopsy and inspect its available contents and metadata.

### 3. Reconstruct the Financial Events

Review the spreadsheet entries relevant to the case.

The exercise focuses on identifying:

- Transactions associated with the victim's account.
- Financial movements described in the spreadsheet.
- Beneficiary accounts identified in the investigation.
- Relationships between the transaction records and the alleged fraud.

Correlate the spreadsheet information with the other evidence available in the forensic case.

## Expected Result

The `lucros.xls` artifact provides information used in the reconstruction of the financial fraud scenario, including the fraudulent transfers and the identification of beneficiary accounts described in the course case.

## Evidence

**Required screenshot: Print 2 - PDF page 2.**

The screenshot must show the Autopsy interface on Windows with the recovered `lucros.xls` spreadsheet open and the relevant details supporting the reconstruction of the case.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Autopsy organizes digital evidence into cases and data sources.
- Recovered files should be examined in the context of their source image and associated metadata.
- Spreadsheet contents should be correlated with other evidence before conclusions are drawn.
- Financial records and account information are sensitive investigative material and must not be published in the repository.
- The evidence included in the course PDF documents the training scenario, not a real-world allegation.

## References

- [Autopsy - Quick Start Guide](https://sleuthkit.org/autopsy/docs/user-docs/4.22.0/quick_start_guide.html)
- [Autopsy - Timeline Documentation](https://sleuthkit.org/autopsy/docs/user-docs/4.22.0/timeline_page.html)

## Navigation

- [Class 01 - Aula 11](../README.md)
- [Previous Activity - 11.1](../atividade-11.1-linha-do-tempo-mactime/README.md)
- [Next Activity - 11.3](../atividade-11.3-john-the-ripper/README.md)
