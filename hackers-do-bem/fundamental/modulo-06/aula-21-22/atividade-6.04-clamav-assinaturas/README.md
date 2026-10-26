# Activity 6.04 — Exploring ClamAV and Its Malware Signatures on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 21–22  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity introduces **ClamAV**, an open-source antivirus engine used on Linux systems, focusing on the `clambc` and `sigtool` utilities.

The laboratory also covers how malware signatures work and how signatures can reference known vulnerabilities, using **CVE-2017-12099** as an example.

The activity focused on analysis and identification. No malware was executed.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`

The credentials used in the laboratory are not recorded in this document.

## 1. Open the Terminal

After accessing Kali Linux through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

## 2. Explore `clambc`

The first command used was:

```bash
clambc -h
```

`clambc` is a ClamAV utility designed for testing **bytecode**, allowing users to inspect and analyze bytecode signatures.

The output displayed in the laboratory was:

```text
                       Clam AntiVirus: Bytecode Testing Tool 1.4.3
          By The ClamAV Team: https://www.clamav.net/about.html#credits
          (C) 2024 Cisco Systems, Inc.

   clambc <file> [function] [param1 ...]

   --help                 -h         Show this help
   --version              -V         Show version
   --debug                           Show debug
   --force-interpreter    -f         Force using the interpreter instead of the JIT
   --trust-bytecode       -t         Trust loaded bytecode (default yes)
   --info                 -i         Print information about bytecode
   --printsrc             -p         Print bytecode source
   --printbcir            -c         Print IR of bytecode signature
   --input                -c         Input file to run the bytecode on
   --trace <level>        -T         Set bytecode trace level 0..7 (default 7)
   --no-trace-showsource  -s         Don't show source line during tracing
   --statistics=bytecode             Collect and print bytecode execution statistics
   file                              File to test

Caution: You should NEVER run bytecode signatures from untrusted sources.
Doing so may result in arbitrary code execution.
```

The utility itself displays an important warning: bytecode signatures from untrusted sources should never be executed because doing so may result in arbitrary code execution.

### Main Options Observed

Some of the options available in `clambc` include:

- `-h` — displays the help information.
- `-V` — displays the version.
- `-i` — prints information about bytecode.
- `-p` — prints the bytecode source code.
- `-c` — prints the intermediate representation of a bytecode signature, as shown in the help output.
- `-T` — sets the tracing level.
- `-f` — forces the use of the interpreter instead of the JIT compiler.

The option descriptions above reflect the recorded help output. The displayed help assigns `-c` to two options, so its precise behavior should be checked against the installed version's documentation before relying on it in automation.

## 3. Explore `sigtool`

Next, the help information for `sigtool` was requested:

```bash
sigtool -h
```

`sigtool` is a utility included with ClamAV for working with signatures, databases, and information related to the detection engine.

Its functions include operations related to creating, inspecting, and manipulating signatures used by ClamAV.

This tool helps demonstrate that threat detection depends not only on the presence of a malicious file, but also on the patterns and information used by an antivirus engine to identify particular artifacts.

## 4. List Bytecode Signatures

To inspect the available signatures, the following command was executed:

```bash
sigtool --list-sigs
```

The output included several signatures associated with exploits and other types of threats.

Examples observed included:

```text
BC.Legacy.Exploit.CVE_2010_3333-5.{Exploit-CVE_2010_3333}
BC.Legacy.Exploit.CVE_2011_0090-1.{Exploit-CVE_2011_0090}
BC.Win.Packer.script2exe-6754169-0.{}
BC.Legacy.Exploit.CVE_2011_0086-1.{Exploit-CVE_2011_0086}
BC.Legacy.Exploit.CVE_2011_4373-2
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
...
```

The listing demonstrates that ClamAV includes signatures associated with different threat categories, including exploits identified by **CVE (Common Vulnerabilities and Exposures)** identifiers.

This output shows that the signatures are present in the listing. It does not, by itself, demonstrate that a particular file was scanned, detected, or classified as malicious.

## 5. Analyze the Signature Associated with CVE-2017-12099

One of the signatures observed was:

```text
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
```

The name contains several descriptive elements:

```text
BC
│
└── Bytecode signature category

Img
│
└── Signature category label

Exploit
│
└── Indicates an exploit-related signature

CVE_2017_12099
│
└── Identifier of the referenced vulnerability
```

These labels provide clues about the signature's classification. The signature name alone does not fully describe the detection logic or prove that a particular exploit was detected.

The CVE identifier provides a reference to publicly documented vulnerability information.

**Technical clarification:** CVE-2017-12099 describes an integer overflow vulnerability in Blender 2.78c involving the upgrade of the legacy Mesh attribute `tface`. A specially crafted `.blend` file could trigger an integer overflow that results in a buffer overflow and may allow code execution when processed by the vulnerable application. This is a vulnerability in Blender, not a vulnerability in ClamAV itself.

Reference: [Cisco Talos — TALOS-2017-0451: Blender Integer Overflow Code Execution Vulnerability](https://talos.talosintelligence.com/vulnerability_reports/TALOS-2017-0451).

## 6. Identify the Type of Attack

For **CVE-2017-12099**, the activity required consulting vulnerability references and identifying the associated attack type.

The attack type identified in the laboratory was:

```text
Integer Overflow
```

**This is the step specified for the activity evidence.**

### Integer Overflow

An **integer overflow** occurs when an arithmetic operation produces a value outside the range representable by the integer type being used.

Under certain conditions, this can have security consequences when the resulting value is subsequently used in operations such as:

- Size calculations.
- Memory allocation.
- File processing.
- Data copying.
- Bounds checking.

In a vulnerable application, an incorrect calculation caused by an overflow can contribute to memory corruption or other unexpected behavior.

In the case of CVE-2017-12099, the documented integer overflow in Blender can result in a buffer overflow when a specially crafted `.blend` file is processed. See the [Cisco Talos vulnerability report](https://talos.talosintelligence.com/vulnerability_reports/TALOS-2017-0451).

## 7. Relationship Between CVEs and Antivirus Signatures

This activity demonstrates an important relationship between vulnerability databases and detection mechanisms.

A **CVE** provides a standardized identifier for a publicly known vulnerability, while a ClamAV signature may be designed to detect artifacts associated with a particular threat or exploit.

In the observed example:

```text
CVE-2017-12099
       │
       ▼
Documented vulnerability
       │
       ▼
Related exploit or artifact
       │
       ▼
ClamAV signature
BC.Img.Exploit.CVE_2017_12099-6336630-0.{}
```

This relationship can help analysts correlate vulnerability information, threats, and detection mechanisms during an investigation.

However, the presence of a CVE identifier in a signature name does not establish that the vulnerable application is installed on the system or that a corresponding exploit has been detected. It identifies the association represented by the signature's naming.

## 8. Research Other Exploits

As part of the activity, other signatures and vulnerabilities identified by CVE were examined.

The output from:

```bash
sigtool --list-sigs
```

included examples such as:

```text
BC.Legacy.Exploit.CVE_2010_3333-5.{Exploit-CVE_2010_3333}
BC.Legacy.Exploit.CVE_2011_0090-1.{Exploit-CVE_2011_0090}
BC.Legacy.Exploit.CVE_2011_0086-1.{Exploit-CVE_2011_0086}
BC.Legacy.Exploit.CVE_2011_4373-2
```

These identifiers show how different vulnerabilities can be referenced by specific signatures.

Using CVEs as references also facilitates correlation between security tools, public vulnerability databases, and research information.

## Concepts Practiced

### ClamAV

**ClamAV** is an open-source antivirus engine used primarily on Unix and Linux systems.

It uses different signature types and analysis mechanisms to identify files and content associated with known threats.

### Malware Signature

A signature represents information used to recognize specific patterns associated with a threat.

In ClamAV, signatures can be associated with different file categories, exploits, and other artifacts. The presence of a signature in a database does not by itself establish that a file has been detected.

### Bytecode

Bytecode is an intermediate form of code that can be used by the ClamAV engine to implement certain checks.

The `clambc` utility provides functions for testing and analyzing this type of signature.

**Security warning:** As indicated by the tool's own help output, bytecode from untrusted sources must not be executed because it may result in arbitrary code execution.

### CVE

**CVE (Common Vulnerabilities and Exposures)** is a system used to identify publicly known security vulnerabilities.

The example used in this activity was:

```text
CVE-2017-12099
```

This CVE concerns an integer overflow vulnerability in Blender 2.78c, as documented in the [Cisco Talos vulnerability report](https://talos.talosintelligence.com/vulnerability_reports/TALOS-2017-0451).

### Integer Overflow

An integer overflow occurs when an integer calculation exceeds the representable range of the type being used.

In information security, this type of error can become significant when the resulting value affects memory operations, size calculations, or data processing.

## Results

The activity provided hands-on exploration of ClamAV tools related to signatures and bytecode.

The following tasks were performed:

1. Obtained administrative access to Kali Linux.
2. Consulted the `clambc` help information.
3. Consulted the `sigtool` help information.
4. Listed the available signatures.
5. Identified signatures associated with CVEs.
6. Located the signature associated with `CVE-2017-12099`.
7. Researched the referenced vulnerability.
8. Identified the attack type as **Integer Overflow**.
9. Examined other exploit signatures referencing CVEs.

The exercise demonstrated how antivirus signatures can be associated with documented vulnerabilities and known exploits, and how analysts can use these references during security investigations.

No malware was executed during the activity.

## Evidence

The evidence for this activity corresponds to **Step 6**, documenting the identification of the attack type associated with `CVE-2017-12099`.

[View Evidence — Classes 21–22](../evidencias.pdf)

---

[Back to Classes 21–22](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
