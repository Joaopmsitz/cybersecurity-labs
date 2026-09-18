# Atividade 6.5 — Automação de Tarefas com PowerShell no Windows Server

## Objetivo

Nesta atividade foi utilizada a **PowerShell** para automatizar tarefas de administração e coleta de informações em um ambiente Windows Server.

Foram desenvolvidos dois scripts:

1. um script para coletar informações do sistema e do hardware;
2. um script para consultar eventos relacionados à inicialização do sistema e gerar um relatório em arquivo.

A atividade demonstra como a PowerShell pode ser utilizada para automatizar tarefas de inventário e análise de eventos em ambientes Windows.

---

## Ambiente

* **Sistema:** Windows Server 2022 Datacenter
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.30`
* **Computador:** `WINCLIENT`
* **Usuário:** `WINSERVER\Administrator`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o Windows PowerShell

Após acessar o Windows Server por RDP, foi aberta a ferramenta **Windows PowerShell** através do menu de aplicativos do sistema.

A PowerShell permite executar comandos e scripts para administração, automação e coleta de informações do Windows.

---

## 2. Coletando informações do sistema e hardware

Foi utilizado o seguinte script:

```powershell id="xzrujn"
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

O script utiliza `Get-CimInstance` para consultar classes do Windows Management Instrumentation (WMI/CIM).

As classes utilizadas foram:

```text id="m6p2v9"
Win32_ComputerSystem
Win32_OperatingSystem
Win32_Processor
Win32_PhysicalMemory
```

Cada classe fornece informações diferentes sobre o sistema.

---

## 3. Resultado da coleta

Após executar os comandos no PowerShell, foram apresentadas as informações do sistema:

```text id="0bimt5"
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

A coleta identificou:

| Informação          | Resultado                                  |
| ------------------- | ------------------------------------------ |
| Computador          | `WINCLIENT`                                |
| Sistema operacional | `Microsoft Windows Server 2022 Datacenter` |
| Arquitetura         | `64-bit`                                   |
| Processador         | `AMD EPYC 7571`                            |

> A saída fornecida no laboratório não apresenta um valor numérico após a linha `Memória Total:`. Por isso, o valor não é reproduzido como um número neste README.

---

## 4. Consultando eventos de inicialização

Em seguida, foi utilizado um segundo script para consultar eventos do log **System** relacionados à inicialização e desligamento do sistema:

```powershell id="lkgd7i"
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

### Funcionamento

Primeiro, o script consulta o log `System`:

```powershell id="u3k7m1"
Get-WinEvent -LogName System
```

Depois, são filtrados os eventos de ID `6005` e `6006`:

```powershell id="n8v4q2"
Where-Object { $_.Id -eq 6005 -or $_.Id -eq 6006 }
```

Esses eventos são utilizados no laboratório para identificar registros relacionados à inicialização e ao desligamento do serviço de log de eventos.

Os dados relevantes são armazenados nas variáveis:

```powershell id="r5x2j9"
$eventTime = $_.TimeCreated
$eventMessage = $_.Message
```

Por fim, as informações são gravadas em:

```text id="w7m3p8"
C:\Relatorio_Eventos_Inicializacao.txt
```

---

## 5. Gerando o relatório

Após executar o segundo script, foi apresentada a seguinte mensagem:

```text id="rohmm8"
Relatório de eventos de inicialização do sistema salvo em C:\Relatorio_Eventos_Inicializacao.txt
```

A mensagem confirma que o relatório foi criado no diretório raiz da unidade `C:`.

---

## 6. Visualizando o relatório

O **File Explorer** foi aberto para acessar:

```text id="f9q4s2"
C:\Relatorio_Eventos_Inicializacao.txt
```

O arquivo contém os registros coletados pelo script, organizados com:

```text id="a2m8v6"
Data e Hora: ...
Mensagem: ...
```

Essa estrutura permite consultar os eventos de inicialização/desligamento registrados no log do sistema de forma mais organizada.

---

## 7. Análise dos eventos

O uso de `Get-WinEvent` permite consultar diretamente os logs do Windows através da PowerShell.

Neste exercício, o script filtrou eventos específicos do log `System`, evitando a necessidade de localizar manualmente cada registro pela interface gráfica.

A automação é especialmente útil em administração e análise de sistemas porque permite:

* consultar grandes quantidades de eventos;
* aplicar filtros;
* extrair campos específicos;
* gerar relatórios;
* repetir o procedimento de forma consistente.

Em um contexto de segurança, logs de sistema também podem auxiliar na investigação de eventos relacionados ao funcionamento e à disponibilidade de uma máquina.

---

## 8. Removendo o relatório

Após visualizar o relatório, o arquivo:

```text id="v6k1p4"
C:\Relatorio_Eventos_Inicializacao.txt
```

foi excluído utilizando **Shift + Delete**.

Em seguida, o File Explorer e o Windows PowerShell foram fechados.

**Este é o passo solicitado para a evidência da atividade.**

---

## Conceitos envolvidos

### PowerShell

A PowerShell é uma ferramenta de automação e gerenciamento desenvolvida pela Microsoft.

Além de comandos interativos, ela permite criar scripts para automatizar tarefas administrativas e trabalhar diretamente com objetos do sistema operacional.

### CIM

O **Common Information Model (CIM)** fornece uma forma padronizada de consultar informações de gerenciamento do sistema.

Na atividade, `Get-CimInstance` foi utilizado para consultar informações sobre:

```text
Sistema
Sistema operacional
Processador
Memória
```

### Get-WinEvent

O cmdlet:

```powershell
Get-WinEvent
```

permite consultar eventos armazenados nos logs do Windows.

No laboratório, foi utilizado:

```powershell
Get-WinEvent -LogName System
```

para consultar o log do sistema.

### Where-Object

O `Where-Object` permite filtrar objetos de acordo com uma condição.

Neste exercício:

```powershell
Where-Object { $_.Id -eq 6005 -or $_.Id -eq 6006 }
```

foi utilizado para selecionar apenas os eventos com os IDs especificados.

### Out-File

O `Out-File` permite direcionar a saída para um arquivo.

No laboratório, foi utilizado:

```powershell
Out-File -Append -FilePath $reportFile
```

para adicionar os dados ao relatório.

---

## Resultado

A atividade demonstrou duas aplicações de automação com PowerShell.

Primeiro, foi realizada uma coleta de informações do sistema e hardware, identificando:

```text
Computador: WINCLIENT
Sistema: Microsoft Windows Server 2022 Datacenter
Arquitetura: 64-bit
Processador: AMD EPYC 7571
```

Depois, foi criado um segundo script para consultar eventos específicos do log `System` e gerar automaticamente o arquivo:

```text
C:\Relatorio_Eventos_Inicializacao.txt
```

A geração do relatório foi confirmada pela saída:

```text
Relatório de eventos de inicialização do sistema salvo em C:\Relatorio_Eventos_Inicializacao.txt
```

Após a visualização, o arquivo foi removido para finalizar a atividade.

---

## Evidência

A evidência desta atividade corresponde ao **passo 8**, após a visualização e remoção do relatório de eventos de inicialização do Windows Server.

[**Evidências — Módulo 6 / Aulas 1 e 2**](../evidencias.pdf)
