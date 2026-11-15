# Activity 11.2 — Reconstruction of Events with Autopsy

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 01  
> **Course Lesson:** 11  
> **Environment:** Windows forensic workstation  
> **Status:** Completed

## 1. Objective

Examine a recovered Microsoft Excel spreadsheet named `lucros.xls` using Autopsy and reconstruct the financial activity represented in the file.

The activity is part of a forensic case study involving suspicious financial transactions.

The objective is to inspect the recovered spreadsheet, identify records associated with fraudulent transfers, and correlate the transaction information with beneficiary accounts.

Autopsy is used as the forensic examination platform to locate and inspect the recovered artifact.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | Windows |
| Forensic Application | Autopsy |
| Evidence File | `lucros.xls` |
| File Type | Microsoft Excel spreadsheet |
| Investigation Type | Financial artifact examination |
| Main Objective | Identify suspicious transfers and beneficiary accounts |
| Evidence Source | Recovered data supplied by the course |

The exact source image, case name, and full path of `lucros.xls` are not included in the activity information available for this documentation.

## 3. Digital Investigation Concepts

### Recovered Files

During a forensic investigation, files recovered from seized storage devices can provide information about user activity and events relevant to a case.

The analysis may involve documents, spreadsheets, databases, images, logs, and other artifacts.

A recovered file should be examined in context, including its name, path, metadata, contents, and relationship with other evidence.

### Autopsy

Autopsy is a graphical digital forensic platform built on The Sleuth Kit.

It supports the creation of forensic cases, addition of evidence sources, file examination, and execution of ingest modules.

A case organizes the data sources and results associated with an investigation.

### Spreadsheet Analysis

Spreadsheets can contain structured records that help reconstruct financial activity.

Relevant information can include:

- Transaction dates.
- Transfer amounts.
- Originating accounts.
- Beneficiary accounts.
- Transaction descriptions.
- Other fields associated with the financial records.

The analysis must consider the relationship between the transaction fields rather than relying only on the filename or isolated values.

### Case Reconstruction

Case reconstruction involves correlating artifacts to establish a sequence of events and identify relationships between people, accounts, files, and transactions.

In this activity, the focus is the relationship between the recovered spreadsheet and the suspected fraudulent transfers.

## 4. Procedure

### Step 1 — Open Autopsy

The forensic workstation was accessed and Autopsy was opened.

Autopsy provides the interface used to create a case and examine the evidence supplied for the investigation.

A forensic case is required before adding and analyzing a data source.

### Step 2 — Create or Open the Forensic Case

The investigation was organized within an Autopsy case.

A new case can be created through the application menu:

```text
Case → New Case
```

The case wizard requests information such as the case name and the base directory used to store case data.

The case provides the structure in which the evidence source and examination results are maintained.

The exact case name and storage path used in the training environment were not included in the available activity notes.

### Step 3 — Add the Evidence Source

After opening the case, the evidence source containing the recovered data was added to Autopsy.

The application provides the following menu path:

```text
Case → Add Data Source
```

Autopsy supports several types of data sources, including disk images, local disks, and logical files.

The source type must correspond to the evidence supplied by the course.

The exact source path and source type selected during the laboratory execution are not reproduced here because they were not included in the activity summary.

### Step 4 — Configure Evidence Processing

During data source addition, Autopsy provides the option to configure ingest modules.

Ingest modules process the source data and can identify or extract information useful during the investigation.

The available modules depend on the installed Autopsy version and the selected data source.

The processing stage allows the examiner to build an index of the available files and examine the relevant artifacts.

### Step 5 — Locate the Recovered Spreadsheet

After the data source was available in the case, the recovered spreadsheet was located:

```text
lucros.xls
```

The filename was identified as the main artifact for this activity.

The spreadsheet was then selected for examination in Autopsy.

The file should be interpreted as a recovered artifact from the supplied forensic dataset rather than as an ordinary document unrelated to the case.

### Step 6 — Examine the Spreadsheet Contents

The contents of `lucros.xls` were examined to identify financial records relevant to the investigation.

The analysis focused on the transactions represented in the spreadsheet and the accounts associated with those transfers.

The main investigative questions were:

1. Which transactions appeared suspicious?
2. What transfer values were recorded?
3. Which accounts were associated with the transfers?
4. Which beneficiary accounts received the amounts?
5. Could the records support a reconstruction of the suspected financial activity?

The activity identified fraudulent transfers and their beneficiary accounts.

The actual transaction rows, dates, monetary values, and account identifiers are not included in the activity summary provided for this README. They should be transcribed from the original spreadsheet or evidence screenshot rather than replaced with invented values.

## 5. Expected Results

The expected result is the identification of the recovered spreadsheet and examination of its financial records.

The activity's findings include:

| Artifact | Finding |
|---|---|
| `lucros.xls` | Recovered spreadsheet examined in Autopsy |
| Financial records | Transactions associated with the investigation |
| Suspicious transfers | Transfer records identified as relevant to the case |
| Beneficiary accounts | Accounts associated with the destination of the transfers |

The findings help support the reconstruction of the financial fraud scenario described in the case study.

## 6. Technical Analysis

### Why Use Autopsy?

Autopsy provides a structured environment for managing forensic cases and examining evidence sources.

Instead of opening isolated files without context, the investigator can organize data sources and analysis results within a case.

This helps preserve the relationship between the original evidence and the findings produced during examination.

### Evidence Source and Ingest

Autopsy distinguishes between adding a data source and processing its contents.

When a data source is added, the application enumerates the files and can run selected ingest modules to analyze them.

The data source must remain accessible while the case references it.

The ingest process does not replace manual examination. It assists the investigator by organizing and processing available artifacts.

### Spreadsheet as a Forensic Artifact

A spreadsheet can provide a structured view of financial activity.

However, the investigator should not assume that every transaction is fraudulent simply because it appears in a file associated with the case.

The records need to be examined for consistency, relationships, timestamps, beneficiary information, and supporting evidence.

A reliable reconstruction should preserve the original values and correlate them with independent evidence whenever available.

### Reconstruction of Financial Transfers

A transaction can be understood by considering both its originating and destination accounts.

Identifying beneficiary accounts helps determine where funds were directed.

When multiple transfers share dates, destinations, descriptions, or other attributes, these relationships can support a broader reconstruction of the activity.

The exercise uses `lucros.xls` to demonstrate this process.

## 7. Results and Interpretation

The activity demonstrates the use of Autopsy to examine a recovered spreadsheet as part of a digital forensic investigation.

The file `lucros.xls` was identified and examined for financial records associated with the case.

The investigation focused on fraudulent transfers and the beneficiary accounts involved.

The findings provide information that can be correlated with other evidence to reconstruct the financial activity under investigation.

The exercise demonstrates that recovered documents can contain important investigative information even when they are not executable files or traditional system artifacts.

## 8. Concepts Practiced

- Digital forensic case management
- Autopsy
- The Sleuth Kit
- Evidence source management
- Ingest processing
- Recovered file examination
- Microsoft Excel artifacts
- Spreadsheet analysis
- Financial transaction analysis
- Beneficiary account identification
- Case reconstruction
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 2 — PDF page 2.**

The screenshot should show the Autopsy examination of the recovered `lucros.xls` spreadsheet.

The evidence should support the reconstruction of the fraudulent transfers and the identification of beneficiary accounts.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 11.2 is on page 2 of the consolidated PDF.

## References

- [Autopsy — Official Documentation](https://www.sleuthkit.org/autopsy/docs/)
- [Autopsy — Data Sources](https://www.sleuthkit.org/autopsy/docs/user-docs/4.17.0/ds_page.html)
- [Autopsy — Cases](https://sleuthkit.org/autopsy/docs/user-docs/4.4/cases_page.html)
- [Autopsy — Ingest Modules](https://sleuthkit.org/autopsy/docs/user-docs/4.4/ingest_page.html)

---

[Back to Class 01](../README.md) · [Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
