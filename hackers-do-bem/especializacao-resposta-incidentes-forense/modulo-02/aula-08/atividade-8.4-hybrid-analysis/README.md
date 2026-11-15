# Activity 8.4 - Malware Analysis with Hybrid Analysis

## Overview

This activity uses Hybrid Analysis to submit the training PDF sample for automated sandbox inspection. The resulting report provides an overview of the file's classification and observed behavior in the selected analysis environment.

## Objectives

- Access the Hybrid Analysis platform.
- Submit the provided `testpdf.pdf` training sample.
- Select an available sandbox environment.
- Generate and inspect a public analysis report.

## Environment

| Component | Description |
|---|---|
| Virtual Machine | `forenseLinux` |
| Online Service | Hybrid Analysis |
| Sample File | `/opt/Desktop/testpdf.pdf` |
| Analysis Type | Automated sandbox analysis |

## Procedure

### 1. Open Hybrid Analysis

Access the service:

- https://www.hybrid-analysis.com/

### 2. Submit the Training Sample

Use the sample file from the previous activity:

```text
/opt/Desktop/testpdf.pdf
```

In the web interface:

1. Select the file upload area.
2. Choose `testpdf.pdf`.
3. Start the analysis.
4. Accept the platform's applicable terms.
5. Select an available analysis environment.
6. Choose **Generate Public Report**, as specified by the training exercise.

### 3. Review the Analysis Report

After processing completes, inspect the report for:

- Threat classification.
- Selected sandbox environment.
- Behavioral indicators.
- Suspicious activities identified by the analysis.
- Additional file metadata and detection information.

## Expected Result

Hybrid Analysis produces a report for `testpdf.pdf` describing the sandbox environment and the behaviors or indicators identified during analysis.

## Evidence

**Required screenshot: Step 2 - Print 4, PDF page 4.**

The screenshot must show the Hybrid Analysis public report for `testpdf.pdf`, including the threat assessment, selected sandbox environment, and suspicious behavior details.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Automated sandbox results are indicators that require analyst interpretation.
- A low or high threat score should not be treated as a complete verdict without reviewing the report details.
- Public reports may expose submitted samples and their analysis results. Do not upload confidential, proprietary, personal, or otherwise sensitive documents.
- Use only the approved training sample in this exercise.

## References

- [Hybrid Analysis](https://www.hybrid-analysis.com/)
- [CrowdStrike - Sandbox Scryer](https://www.crowdstrike.com/en-us/blog/sandbox-scryer-free-threat-hunting-tool/)

## Navigation

- [Class 08](../README.md)
- [Previous Activity - 8.3](../atividade-8.3-analise-malware-pdf/README.md)
- [Next Activity - 8.5](../atividade-8.5-analise-memoria-volatility/README.md)
