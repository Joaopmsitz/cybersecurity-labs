# Lab 04 - Skills Assessment

## Objective

Analyze historical Windows Event Logs and Sysmon telemetry to investigate suspicious endpoint activity and identify processes involved in different attack techniques.

---

## Investigation Scenarios

### 1. DLL Hijacking

- Investigate Sysmon Event ID 7 (Image Loaded).
- Identify suspicious DLL loading activity.
- Examine image paths, DLL paths, digital signatures, and process relationships.

### 2. Unmanaged PowerShell Execution

- Investigate .NET runtime DLL loading.
- Monitor `clr.dll` and `clrjit.dll`.
- Identify processes executing .NET-related code in unusual contexts.

### 3. Process Injection

- Investigate Sysmon Event ID 8 (CreateRemoteThread).
- Analyze `SourceImage` and `TargetImage`.
- Identify the process responsible for injection and its target.

### 4. LSASS Dump

- Investigate Sysmon Event ID 10 (Process Access).
- Identify processes accessing `lsass.exe`.
- Examine `SourceImage`, `TargetImage`, `GrantedAccess`, and `CallTrace`.

### 5. Suspicious Authentication

- Examine Security Event ID 4624 (Successful Logon).
- Correlate authentication events with the LSASS access timeline.
- Review account, LogonType, source address, and timestamp.

### 6. Strange Parent-Child Relationships

- Investigate Sysmon Event ID 1 (Process Create).
- Examine `Image`, `ParentImage`, `CommandLine`, and `ParentCommandLine`.
- Identify anomalous process creation behavior.

---

## Investigation Methodology

1. Enumerate available EVTX files.
2. Query relevant events using PowerShell `Get-WinEvent`.
3. Filter events by Event ID and relevant properties.
4. Correlate timestamps and process relationships.
5. Validate suspicious activity using available telemetry.
6. Document findings based on collected evidence.

---

## Key Takeaways

- Event correlation is essential for reconstructing attack activity.
- Sysmon provides valuable process, image loading, and process access telemetry.
- Event IDs help investigate specific attack techniques.
- Parent-child relationships can reveal suspicious execution behavior.
- Authentication events provide additional context during incident investigations.

---

## Assessment Notes

The original assessment answers are intentionally omitted from this public documentation.
