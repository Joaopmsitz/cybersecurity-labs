# Activity 11.5 — Steganography Analysis with Steghide

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 01  
> **Course Lesson:** 11  
> **Environment:** Linux forensic environment  
> **Status:** Completed

## 1. Objective

Extract and examine hidden information embedded in a JPEG image using Steghide.

The activity uses the image:

```text
fun.jpg
```

The `steghide` utility is used to extract the embedded data from the image.

The extracted file is:

```text
festa.txt
```

The objective is to demonstrate how steganography can be used to conceal data within an ordinary-looking image and how forensic tools can recover the embedded information.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | Linux |
| Steganography Tool | Steghide |
| Input Image | `fun.jpg` |
| Image Type | JPEG |
| Operation | Data extraction |
| Extraction Command | `steghide --extract -sf fun.jpg` |
| Recovered File | `festa.txt` |
| Output Type | Extracted embedded data |

The exact source directory of `fun.jpg` and the embedded content of `festa.txt` are not included in the activity notes available for this documentation.

## 3. Steganography Concepts

### Steganography

Steganography is the practice of concealing information within another file or communication medium.

Unlike encryption, which transforms information into an unreadable representation, steganography attempts to hide the existence of the information itself.

A digital image can act as a cover file that contains additional embedded data.

### Cover File and Stego File

The original image used to carry hidden information is commonly referred to as a cover file.

After data has been embedded, the resulting file is referred to as a stego file.

For this activity, the image supplied for examination is:

```text
fun.jpg
```

The objective is to determine whether embedded content can be extracted from the image.

### Steghide

Steghide is a steganography utility that supports embedding and extracting data from supported cover-file formats, including JPEG images.

The tool provides commands to embed data, extract embedded content, and inspect information about a cover or stego file.

The activity uses the extraction functionality.

### Embedded Filename

Steghide can preserve the original filename associated with the embedded data.

When extracting without explicitly specifying another output filename, the tool can save the recovered content under the embedded filename in the current directory.

The file recovered in this activity is:

```text
festa.txt
```

## 4. Procedure

### Step 1 — Identify the Image

The image supplied for the activity was:

```text
fun.jpg
```

The file was used as the input to the steganography extraction procedure.

The image should be preserved as an evidence artifact before analysis.

### Step 2 — Execute the Steghide Extraction Command

The extraction was initiated using:

```bash
steghide --extract -sf fun.jpg
```

The command components are:

| Component | Function |
|---|---|
| `steghide` | Starts the steganography utility |
| `--extract` | Selects the data extraction operation |
| `-sf` | Specifies the stego file |
| `fun.jpg` | Input JPEG image containing the embedded data |

The command instructs Steghide to extract the data embedded in `fun.jpg`.

### Step 3 — Provide the Passphrase if Requested

Depending on how the data was embedded, Steghide may request a passphrase.

The tool displays an interactive prompt:

```text
Enter passphrase:
```

The required passphrase must come from the authorized course exercise or the supplied evidence context.

The exact passphrase is not included in the activity notes available for this documentation and is therefore not reproduced here.

### Step 4 — Identify the Extracted File

After successful extraction, Steghide writes the recovered content to:

```text
festa.txt
```

When no alternative extraction filename is specified, Steghide uses the filename stored with the embedded data.

A successful extraction can produce a confirmation similar to:

```text
wrote extracted data to "festa.txt".
```

The exact wording may vary with the installed version.

### Step 5 — Inspect the Recovered Content

The extracted file was then examined:

```bash
cat festa.txt
```

The `cat` command displays the contents of the recovered text file in the terminal.

This step is important because extracting a hidden file is only the first stage of the examination.

The recovered text must also be inspected to determine whether it contains information relevant to the investigation.

The actual contents of `festa.txt` were not included in the activity notes supplied for this documentation, so no text is invented or attributed to the recovered file.

## 5. Expected Results

The activity successfully extracts the data embedded in the JPEG image.

| Item | Result |
|---|---|
| Input Image | `fun.jpg` |
| Tool | Steghide |
| Operation | Extraction |
| Output File | `festa.txt` |
| Inspection Command | `cat festa.txt` |

The recovered file becomes an additional artifact for forensic examination.

## 6. Technical Analysis

### Hidden Data in Images

Steganography can be used to conceal information within image files.

Because the cover image may still appear to be an ordinary JPEG, basic visual inspection does not necessarily reveal that additional data is embedded.

A forensic examiner may therefore need specialized tools to identify and extract hidden content.

### The `--extract` Option

The command uses:

```bash
steghide --extract
```

This selects the extraction operation.

The tool attempts to recover the embedded data from the supplied stego file.

### The `-sf` Option

The command also uses:

```bash
-sf fun.jpg
```

The `-sf` option identifies the image containing the embedded data.

Steghide processes this file as the source of the extraction.

### Output Filename

The command does not include an explicit extraction filename through `-xf`.

According to the Steghide manual, when no alternative extraction filename is specified, the embedded data is saved under its original embedded filename in the current directory.

In this activity, the recovered filename was:

```text
festa.txt
```

### Importance of Inspecting the Recovered File

Extraction does not establish the meaning or relevance of the hidden content.

The recovered file must be examined independently.

The `cat` command allows the analyst to inspect the text directly in the terminal, after which the contents can be correlated with other evidence from the case.

## 7. Results and Interpretation

The activity demonstrates the use of Steghide to extract hidden information from a JPEG image.

The image `fun.jpg` was processed using:

```bash
steghide --extract -sf fun.jpg
```

The extracted artifact was:

```text
festa.txt
```

The recovered text was then inspected with:

```bash
cat festa.txt
```

This exercise demonstrates that ordinary-looking image files can contain additional data that may be relevant during a forensic investigation.

It also reinforces the importance of preserving both the original image and the extracted artifact so that the relationship between the two can be documented.

## 8. Concepts Practiced

- Digital steganography
- Cover files
- Stego files
- JPEG analysis
- Steghide
- Embedded data extraction
- Passphrase-protected content
- Output filename handling
- Text-file inspection
- Evidence preservation
- Forensic artifact examination

## 9. Evidence

**Required screenshot: Print 5 — PDF page 5.**

The screenshot should show:

- The extraction command `steghide --extract -sf fun.jpg`.
- The extraction process and completion.
- The recovered file `festa.txt`.
- The contents of the recovered text file.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 11.5 is on page 5 of the consolidated PDF.

## References

- [Steghide — Official Project](https://steghide.sourceforge.net/)
- [Steghide — Official Manual](https://steghide.sourceforge.net/documentation/manual.pdf)

---

[Back to Class 01](../README.md) · [Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md)
