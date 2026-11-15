# Activity 4.4 — Converting Playbooks for Incident Response Platforms

## Objective

Complete a Sigma detection rule for the removal of the immutable file attribute using the Linux `chattr` command, then convert the rule into an ElastAlert representation using Uncoder IO.

The exercise demonstrates how a detection use case can be described in a vendor-independent format and translated for use by a security monitoring platform.

## Tools and references

- [SigmaHQ — Rule specification and community rules](https://github.com/SigmaHQ/sigma)
- [Uncoder IO](https://uncoder.io/)
- [Atomic Red Team — T1222.002](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1222.002/T1222.002.md)

## 1. Detection scenario

The exercise is based on **Atomic Test #9 — chattr: Remove immutable file attribute**, associated with the MITRE ATT&CK sub-technique **T1222.002**.

The command used in the Atomic test is:

    chattr -i /var/spool/cron/root

The `chattr` utility changes file attributes on supported Linux filesystems. The `-i` option removes the immutable attribute from a file.

Removing this attribute can allow subsequent modification or deletion of a file that was previously protected against those operations. In an incident investigation, this behavior may be suspicious when it affects sensitive system files or occurs without an authorized administrative reason.

## 2. Sigma rule

The exercise required completing the following sections:

- `title`
- `description`
- `references`
- `author`
- `date`
- `tags`
- `logsource`
- `detection/selection`

The following YAML is a documented reconstruction of the detection logic from the exercise instructions and Atomic Test #9. It illustrates the intended rule; compare its metadata and exact field values with the activity screenshot if a verbatim copy of the submitted rule is required.

    title: Linux Immutable Attribute Removal with Chattr
    status: test
    description: Detects execution of chattr with the -i option to remove the immutable file attribute.
    references:
        - https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1222.002/T1222.002.md
    author: João Paulo Moreira de Sousa
    date: 2026/05/11
    tags:
        - attack.defense_evasion
        - attack.t1222.002
    logsource:
        product: linux
        category: process_creation
    detection:
        selection:
            Image|endswith: chattr
            CommandLine|contains: '-i'
        condition: selection
    falsepositives:
        - Administrator interacting with immutable files (e.g. for instance backups).
    level: medium

### Rule structure

| Section | Purpose |
|---|---|
| `title` | Identifies the detection use case |
| `status` | Indicates that the rule is in test status |
| `description` | Explains the behavior the rule detects |
| `references` | Links the rule to its technical source |
| `author` | Identifies the rule author |
| `date` | Records the rule date |
| `tags` | Associates the rule with ATT&CK tactics and techniques |
| `logsource` | Defines the expected event source |
| `detection` | Describes the event selection and matching condition |
| `falsepositives` | Documents legitimate activity that may match the rule |
| `level` | Defines the rule's severity level |

### Detection logic

The selection looks for process creation events in Linux logs where:

1. The executed image ends with `chattr`.
2. The command line contains `-i`.

The `condition: selection` clause requires the defined selection to match.

The rule can identify a potentially suspicious action, but it does not independently establish malicious intent. Authorized administrators may legitimately change immutable attributes during maintenance or backup operations. The alert must therefore be investigated in context.

## 3. Convert Sigma to ElastAlert

The completed Sigma rule was submitted to [Uncoder IO](https://uncoder.io/) for conversion.

Procedure:

1. Open Uncoder IO.
2. Insert the Sigma rule into the source editor.
3. Select the Sigma input format when required.
4. Select ElastAlert as the target format.
5. Run the conversion.
6. Review the generated output and identify the corresponding detection query and rule configuration.
7. Capture the conversion result.

The activity report confirms that the Sigma rule was converted to ElastAlert using Uncoder IO.

## 4. Technical considerations

Sigma provides a generic description of a detection use case. It does not eliminate the need to adapt the generated query to the destination platform.

Before deploying a converted rule, analysts should validate:

- Whether the target data source records process creation events.
- Whether the event schema contains the fields used by the detection.
- Whether command-line arguments are collected and normalized.
- Whether the generated query is compatible with the intended Elasticsearch environment.
- Whether legitimate administrative activity requires exclusions or additional context.
- Whether the alert severity and response workflow are appropriate.

A converted rule should be tested against representative events before being enabled in production.

## Result

The activity completed the detection use case for `chattr -i` and used Uncoder IO to convert the Sigma representation into an ElastAlert rule.

The exact converted query is not reproduced here because its complete text was not included in the activity report. The conversion evidence is preserved in the universal class PDF.

## Evidence

[View Universal Class Evidence PDF — Page 3](../evidences.pdf)
