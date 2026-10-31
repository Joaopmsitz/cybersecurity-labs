
# <img src="./images/windows-event-logs-finding-evil.png" width="36" alt="Windows Event Logs & Finding Evil"> Windows Event Logs & Finding Evil

> HTB Academy — SOC Analyst Job Role Path (CDSA)

## Overview

This module explores Windows Event Logs, Sysmon, and Event Tracing for Windows (ETW) as sources of endpoint telemetry for security monitoring, threat detection, and incident investigation.

It covers event analysis, log correlation, suspicious activity identification, and PowerShell-based event querying.

---

## Windows Event Logs

Windows Event Logs centralize operating system, application, and security-related activities.

### Default Event Logs

| Log | Description |
|---|---|
| Application | Application-generated events |
| Security | Authentication, auditing, and security events |
| System | Operating system and service events |
| Setup | Installation and configuration events |
| Forwarded Events | Events collected from remote systems |

### Event Anatomy

| Field | Description |
|---|---|
| Log Name | Event log containing the record |
| Source | Component that generated the event |
| Event ID | Event identifier |
| Level | Severity of the event |
| Keywords | Event classification |
| User | Associated security principal |
| Logged | Event timestamp |
| Computer | Host that generated the event |
| XML Data | Structured event details |

---

## Important Windows Event IDs

| Event ID | Description |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4648 | Logon using explicit credentials |
| 4672 | Special privileges assigned to a new logon |
| 4688 | Process creation |
| 4719 | System audit policy changed |
| 4907 | Auditing settings on an object changed |
| 1102 | Security audit log cleared |

### Event Correlation

Correlating events through identifiers such as Logon ID helps reconstruct activity associated with a particular logon session.

**Event ID 4624 — Successful Logon**

Useful fields:

- TargetUserName
- TargetDomainName
- TargetLogonId
- LogonType
- ProcessName

**Event ID 4907 — Auditing Settings Changed**

Useful fields:

- SubjectLogonId
- ObjectName
- ProcessName
- Original Security Descriptor
- New Security Descriptor

The Logon ID can be used to correlate authentication activity with subsequent object auditing events.

### SACL and Object Auditing

A System Access Control List (SACL) defines which access attempts against an object should be audited.

Event ID 4907 records changes to an object's auditing settings.

Security Descriptor comparisons can help identify modifications to auditing configurations.

---

## XML Event Filtering

Event Viewer supports custom XML queries for more precise filtering.

### Filter by Event ID and Logon ID

```xml
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">
      *[System[(EventID=4907)] and EventData[
        Data[@Name='SubjectLogonId']='0x123456'
      ]]
    </Select>
  </Query>
</QueryList>
```

Replace the example Logon ID with the identifier observed in the investigation.

### Filter by Object Name

```xml
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">
      *[System[(EventID=4907)] and EventData[
        Data[@Name='ObjectName']='C:\Path\To\File'
      ]]
    </Select>
  </Query>
</QueryList>
```

Replace the example path with the object being investigated.

---

## PowerShell — Get-WinEvent

`Get-WinEvent` retrieves event records from Windows event logs and supports filtering by log name, event ID, and time range.

### Retrieve Security Events

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4624, 4907
} -MaxEvents 50 |
Select-Object TimeCreated, Id, ProviderName, Message
```

### Search Events by Logon ID

```powershell
$LogonId = '0x123456'

Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4907
} |
Where-Object {
    $_.Message -match [regex]::Escape($LogonId)
} |
Select-Object TimeCreated, Id, Message
```

### Retrieve Events from a Specific Time Range

```powershell
$Start = Get-Date '2026-01-01 10:00:00'
$End   = Get-Date '2026-01-01 11:00:00'

Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id = 4624, 4907
    StartTime = $Start
    EndTime = $End
} |
Select-Object TimeCreated, Id, Message
```

---

## Investigation Workflow

```text
Identify Relevant Event
          ↓
Inspect Event Details
          ↓
Extract Logon ID
          ↓
Correlate Related Events
          ↓
Inspect Object and Process
          ↓
Validate Timestamp and Evidence
          ↓
Document Findings
```

---

## Lab Environment

### Remote Desktop — FreeRDP

Connect to Windows lab targets from Athena OS using FreeRDP 3.

```bash
xfreerdp3 /v:<TARGET_IP> /u:Administrator /d:. '/auth-pkg-list:none,ntlm' /dynamic-resolution /cert:ignore
```

Credentials should be entered interactively rather than stored in scripts or documentation.

### VPN Connectivity

Check the route to the target:

```bash
ip route get <TARGET_IP>
```

The route should use the active HTB VPN interface.

---

## Lab Evidence

Personal lab evidence is retained locally and excluded from this public repository.

![Windows Event Viewer — XML Filtering](./images/event-viewer-xml-filter.png)

---

## Key Takeaways

- Windows Event Logs provide valuable endpoint security telemetry.
- Event IDs help identify authentication and auditing activities.
- Logon IDs enable correlation between related security events.
- Event ID 4907 records modifications to object auditing settings.
- SACLs define which object access attempts are audited.
- XML queries provide precise event filtering.
- PowerShell Get-WinEvent supports efficient event investigation.
- Event correlation helps reconstruct activity and establish timelines.

---

## Completion

**Status:** In progress

<!-- Add the official badge and completion date after finishing the module.

<a href="OFFICIAL_BADGE_URL">
  <img src="./images/htb-windows-event-logs-finding-evil-badge.png" width="120" alt="HTB Academy — Windows Event Logs & Finding Evil Badge">
</a>

**Completed:** DD Month YYYY
-->

---

## References

- [Hack The Box Academy — Windows Event Logs & Finding Evil](https://academy.hackthebox.com/course/preview/windows-event-logs--finding-evil)
- [Microsoft — Windows Security Auditing](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/)
- [Microsoft — Get-WinEvent](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [Microsoft — Access Control Lists](https://learn.microsoft.com/en-us/windows/win32/secauthz/access-control-lists)
