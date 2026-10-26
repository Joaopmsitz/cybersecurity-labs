# Activity 6.05 — Task Automation with PowerShell on Windows Server

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 21–22  
> **Environment:** Windows Server 2022 Datacenter  
> **Status:** Completed

## Objective

This activity uses PowerShell to automate administrative tasks and information collection in a Windows Server environment.

Two scripts were developed:

- A script to collect system and hardware information.
- A script to query events related to system startup and shutdown and generate a report file.

The activity demonstrates how PowerShell can automate inventory and event analysis tasks in Windows environments.

## Environment

- **Operating system:** Windows Server 2022 Datacenter
- **Access method:** RDP
- **Machine IP address:** `192.168.98.30`
- **Computer name:** `WINCLIENT`
- **User:** `WINSERVER\Administrator`

The credentials used in the laboratory are not recorded in this document.

## Procedure

### 1. Open Windows PowerShell

After accessing Windows Server through RDP, Windows PowerShell was opened from the system's application menu.

PowerShell allows administrators to execute commands and scripts for Windows administration, automation, and information gathering.

### 2. Collect System and Hardware Information

The following script was used:

```powershell
# Coleta informações do sistema e hardware
$systemInfo = Get-CimInstance -ClassName Win32_ComputerSystem
$osInfo = Get-CimInstance -ClassName Win32_OperatingSystem
$cpuInfo = Get-CimInstance -ClassName Win32_Processor
$memoryInfo = Get-CimInstance -ClassName Win32_PhysicalMemory

# Exibe informações no console
Write-Host "Informações do Sistema:"
Write-Host "Nome do Computador: $($systemInfo.Name)"
Write-Host "Sistema Operacional: $($osInfo.Caption)"
Write-Host "Arquitetura do Sistema: $($osInfo.OSArchitecture)"
Write-Host "Processador: $($cpuInfo.Name)"
Write-Host "Memória Total: $($memoryInfo.Capacity / 1GB) GB"
```

The script uses `Get-CimInstance` to query Windows Management Instrumentation and Common Information Model (WMI/CIM) classes.

The classes used were:

```text
Win32_ComputerSystem
Win32_OperatingSystem
Win32_Processor
Win32_PhysicalMemory
```

Each class provides different information about the system.

### 3. Review the Information Collection Results

After executing the commands in PowerShell, the following system information was displayed:

```text
PS C:\Users\Administrator> Write-Host "Informações do Sistema:"
Informações do Sistema:
PS C:\Users\Administrator> Write-Host "Nome do Computador: $($systemInfo.Name)"
Nome do Computador: WINCLIENT
PS C:\Users\Administrator> Write-Host "Sistema Operacional: $($osInfo.Caption)"
Sistema Operacional: Microsoft Windows Server 2022 Datacenter
PS C:\Users\Administrator> Write-Host "Arquitetura do Sistema: $($osInfo.OSArchitecture)"
Arquitetura do Sistema: 64-bit
PS C:\Users\Administrator> Write-Host "Processador: $($cpuInfo.Name)"
Processador: AMD EPYC 7571
PS C:\Users\Administrator> Write-Host "Memória Total: $($memoryInfo.Capacity / 1GB) GB"
```

The collection identified the following information:

| Information | Result |
|---|---|
| Computer | `WINCLIENT` |
| Operating system | Microsoft Windows Server 2022 Datacenter |
| Architecture | 64-bit |
| Processor | AMD EPYC 7571 |

The laboratory output does not show a numeric value after `Memória Total:`. Therefore, no numeric memory total is reported in this README.

**Technical note:** `Win32_PhysicalMemory` can return multiple objects, one for each physical memory module. To calculate the total installed memory reliably, the capacities should be summed before converting the result to gigabytes.

### 4. Query Startup and Shutdown Events

A second script was then used to query events in the System log related to the startup and shutdown of the event logging service:

```powershell
# Coleta informações de eventos de inicialização do sistema
$events = Get-WinEvent -LogName System | Where-Object { $_.Id -eq 6005 -or $_.Id -eq 6006 }

# Caminho para o arquivo de relatório
$reportFile = "C:\Relatorio_Eventos_Inicializacao.txt"

# Gera um relatório e o salva em um arquivo
$events | ForEach-Object {
    $eventTime = $_.TimeCreated
    $eventMessage = $_.Message
    $report = "Data e Hora: $eventTime`nMensagem: $eventMessage`n`n"
    $report | Out-File -Append -FilePath $reportFile
}

Write-Host "Relatório de eventos de inicialização do sistema salvo em $reportFile"
```

#### How the Script Works

First, the script queries the Windows System log:

```powershell
Get-WinEvent -LogName System
```

The events with IDs 6005 and 6006 are then filtered:

```powershell
Where-Object { $_.Id -eq 6005 -or $_.Id -eq 6006 }
```

These event IDs are used in the laboratory to identify records associated with the startup and shutdown of the Windows Event Log service.

The relevant information is stored in the following variables:

```powershell
$eventTime = $_.TimeCreated
$eventMessage = $_.Message
```

Finally, the information is written to:

```text
C:\Relatorio_Eventos_Inicializacao.txt
```

### 5. Generate the Report

After executing the second script, the following message was displayed:

```text
Relatório de eventos de inicialização do sistema salvo em C:\Relatorio_Eventos_Inicializacao.txt
```

The message confirms that the report was created in the root directory of the `C:` drive.

### 6. View the Report

File Explorer was opened to access:

```text
C:\Relatorio_Eventos_Inicializacao.txt
```

The file contains the records collected by the script, organized using the following format:

```text
Data e Hora: ...
Mensagem: ...
```

This structure makes it easier to review startup- and shutdown-related events recorded in the system log.

### 7. Analyze the Events

The `Get-WinEvent` cmdlet allows PowerShell to query Windows event logs directly.

In this exercise, the script filtered specific event IDs from the System log, avoiding the need to locate each record manually through the graphical interface.

Automation is particularly useful for system administration and analysis because it allows administrators to:

- Query large volumes of events.
- Apply filters.
- Extract specific fields.
- Generate reports.
- Repeat procedures consistently.

In a security context, system logs can also support investigations into events related to a machine's operation and availability.

### 8. Remove the Report

After viewing the report, the following file was deleted:

```text
C:\Relatorio_Eventos_Inicializacao.txt
```

The file was removed using **Shift + Delete**.

File Explorer and Windows PowerShell were then closed.

This is the step specified for the activity evidence.

## Concepts Practiced

### PowerShell

PowerShell is an automation and management tool developed by Microsoft.

In addition to interactive commands, it allows administrators to create scripts that automate administrative tasks and interact directly with operating system objects.

### CIM — Common Information Model

The Common Information Model (CIM) provides a standardized way to query system management information.

In this activity, `Get-CimInstance` was used to retrieve information about:

- The system.
- The operating system.
- The processor.
- Physical memory.

### `Get-WinEvent`

The `Get-WinEvent` cmdlet allows users to query events stored in Windows event logs.

In the laboratory, the following command was used to query the System log:

```powershell
Get-WinEvent -LogName System
```

### `Where-Object`

The `Where-Object` cmdlet filters objects according to a specified condition.

In this exercise:

```powershell
Where-Object { $_.Id -eq 6005 -or $_.Id -eq 6006 }
```

was used to select only events with the specified IDs.

### `Out-File`

The `Out-File` cmdlet redirects output to a file.

In the laboratory, the following command was used to append information to the report:

```powershell
Out-File -Append -FilePath $reportFile
```

## Results

The activity demonstrated two PowerShell automation use cases.

First, system and hardware information was collected, identifying:

```text
Computer: WINCLIENT
Operating system: Microsoft Windows Server 2022 Datacenter
Architecture: 64-bit
Processor: AMD EPYC 7571
```

Next, a second script was created to query specific events from the System log and automatically generate the following file:

```text
C:\Relatorio_Eventos_Inicializacao.txt
```

Report generation was confirmed by the output:

```text
Relatório de eventos de inicialização do sistema salvo em C:\Relatorio_Eventos_Inicializacao.txt
```

After the report was viewed, the file was deleted to complete the activity.

The exercise demonstrated how PowerShell can automate system inventory, query Windows event logs, filter records, and generate reports for administrative and security analysis.

## Evidence

The activity evidence corresponds to Step 8, after viewing and deleting the Windows Server startup event report.

[View Evidence — Classes 21–22](../evidencias.pdf)

---

[Back to Classes 21–22](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
