# Atividade 12.2 — Habilitando o NTP no Windows Server 2022

## Objetivo

Configurar o serviço **Windows Time (W32Time)** no Windows Server 2022 para utilizar o **NTP (Network Time Protocol)**, habilitando o servidor e o cliente NTP por meio da Política de Grupo e configurando o servidor `time.google.com`.

Ao final, o estado do serviço será consultado com o comando `w32tm /query /status`.

---

## Ambiente

* **Sistema operacional:** Windows Server 2022
* **Acesso:** RDP
* **Serviço:** Windows Time (`W32Time`)
* **Protocolo:** NTP
* **Servidor NTP configurado:** `time.google.com`

---

## 1. Abrindo o Editor de Política de Grupo

No campo de pesquisa da barra de tarefas do Windows Server 2022, foi digitado:

```text id="f4k8mz"
gpedit.msc
```

Em seguida, foi aberto o **Local Group Policy Editor**.

---

## 2. Acessando as configurações do Windows Time

No Editor de Política de Grupo, foi seguido o caminho:

```text id="j7p2qx"
Computer Configuration
→ Administrative Templates
→ System
→ Windows Time Service
→ Time Providers
```

A seção **Time Providers** contém as configurações relacionadas aos provedores de tempo utilizados pelo Windows.

---

## 3. Habilitando o Windows NTP Server

Na área direita da janela, foi localizada a política:

```text id="w8c3nr"
Enable Windows NTP Server
```

A política foi aberta com duplo clique.

Em seguida:

1. Selecionado **Enabled**.
2. Clicado em **OK**.

Essa configuração habilita a funcionalidade de servidor NTP do Windows.

---

## 4. Habilitando o Windows NTP Client

Na mesma seção, foi localizada a política:

```text id="m5v9kt"
Enable Windows NTP Client
```

A política foi aberta e configurada como:

```text id="x2q6wp"
Enabled
```

Depois, foi clicado em **OK**.

Essa configuração habilita o cliente NTP do Windows para realizar sincronização de horário.

---

## 5. Configurando o servidor NTP

Ainda em **Time Providers**, foi aberta a política:

```text id="r9d4vb"
Configure Windows NTP Client
```

A configuração foi definida como:

```text id="n6x3cz"
Enabled
```

No campo **NtpServer**, foi informado:

```text id="k4p8ws"
time.google.com,0x9
```

Em seguida, foi clicado em **OK**.

O valor `time.google.com` define o servidor de referência configurado para o cliente NTP. O parâmetro `0x9` faz parte da configuração do provedor de tempo do Windows.

---

## 6. Abrindo o PowerShell como administrador

No campo de pesquisa da barra de tarefas, foi digitado:

```text id="c7m2vx"
Windows PowerShell
```

Em seguida, foi clicado com o botão direito sobre **Windows PowerShell** e selecionada a opção:

```text id="z5r9qp"
Run as administrator
```

---

## 7. Reiniciando o serviço Windows Time

Para que as configurações fossem aplicadas ao serviço, foi executado:

```powershell id="b3n7kf"
net stop w32time
```

Resultado:

```text id="6qv2md"
PS C:\Users\Administrator> net stop w32time
The Windows Time service is stopping.
The Windows Time service was stopped successfully.
```

O serviço foi interrompido com sucesso.

---

## 8. Iniciando novamente o Windows Time

Em seguida, o serviço foi iniciado novamente:

```powershell id="h8p4rs"
net start w32time
```

Resultado:

```text id="2m7xvc"
PS C:\Users\Administrator> net start w32time
The Windows Time service is starting.
The Windows Time service was started successfully.
```

O serviço **Windows Time** voltou a funcionar.

---

## 9. Consultando o estado do serviço NTP

Para verificar o estado atual do serviço de horário, foi executado:

```powershell id="v6k3qp"
w32tm /query /status
```

A saída apresentada pelo laboratório foi:

```text id="a4r9xz"
PS C:\Users\Administrator> w32tm /query /status
Leap Indicator: 0(no warning)
Stratum: 1 (primary reference - syncd by radio clock)
Precision: -23 (119.209ns per tick)
Root Delay: 0.0000000s
Root Dispersion: 10.0000000s
ReferenceId: 0x4C4F434C (source name:  "LOCL")
Last Successful Sync Time: 3/18/2024 5:18:04 PM
Source: Local CMOS Clock
Poll Interval: 6 (64s)
```

### Interpretação dos campos

#### Leap Indicator

```text
Leap Indicator: 0(no warning)
```

Indica o estado relacionado a ajustes de segundos intercalares. O valor apresentado não indica nenhum aviso.

#### Stratum

```text
Stratum: 1
```

Representa o nível hierárquico da fonte de tempo indicada pelo serviço.

#### Precision

```text
Precision: -23 (119.209ns per tick)
```

Representa a precisão estimada do relógio do sistema.

#### Root Delay

```text
Root Delay: 0.0000000s
```

Indica o atraso associado à comunicação com a referência de tempo.

#### Root Dispersion

```text
Root Dispersion: 10.0000000s
```

Representa a dispersão estimada em relação à referência de tempo.

#### ReferenceId

```text
ReferenceId: 0x4C4F434C (source name:  "LOCL")
```

Identifica a referência de tempo indicada pelo serviço. Nesse resultado, `LOCL` corresponde à referência local.

#### Last Successful Sync Time

```text
Last Successful Sync Time: 3/18/2024 5:18:04 PM
```

Indica a data e hora registradas pelo serviço como última sincronização bem-sucedida.

#### Source

```text
Source: Local CMOS Clock
```

Indica que, **no resultado apresentado**, a fonte de tempo reportada pelo serviço era o relógio local.

Isso é importante porque a atividade configura `time.google.com`, mas a saída fornecida pelo laboratório **não demonstra que a sincronização efetiva naquele momento tenha ocorrido com o servidor do Google**. A configuração e o estado efetivamente reportado pelo `w32tm` são informações distintas.

#### Poll Interval

```text
Poll Interval: 6 (64s)
```

Indica o intervalo utilizado para as consultas de sincronização.

---

## 10. Evidência

O print obrigatório corresponde ao **passo 10**, mostrando a saída do comando:

```powershell
w32tm /query /status
```

**Frase obrigatória antes do print:**

> **Print da atividade 12.2:** saída do comando `w32tm /query /status` no Windows Server 2022, exibindo o estado atual do serviço Windows Time e os parâmetros relacionados à sincronização de horário.

[**Evidências — Módulo 12 / Aulas 45 e 46**](../evidencias.pdf)

---

## 11. Encerramento

Após a consulta do estado do serviço, as janelas utilizadas na atividade foram fechadas.

---

## Conceitos

* **NTP (Network Time Protocol):** protocolo utilizado para sincronização de relógios em redes.
* **W32Time:** serviço do Windows responsável pelas funcionalidades de sincronização de horário.
* **NTP Client:** componente utilizado pelo Windows para consultar fontes de tempo.
* **NTP Server:** funcionalidade que permite ao Windows atuar como fonte de tempo para outros clientes.
* **`w32tm`:** ferramenta de linha de comando utilizada para configurar e consultar o serviço Windows Time.
* **Stratum:** indica a posição hierárquica de uma fonte de tempo dentro da infraestrutura NTP.

## Fluxo

```text
Configuração da Política de Grupo
              ↓
Enable Windows NTP Server
              ↓
Enable Windows NTP Client
              ↓
Configure Windows NTP Client
              ↓
time.google.com,0x9
              ↓
Reiniciar W32Time
              ↓
w32tm /query /status
              ↓
Consultar estado do serviço
```

## Resultado

O Windows Server 2022 foi configurado para habilitar as funcionalidades de cliente e servidor NTP, com `time.google.com,0x9` definido como servidor NTP. O serviço **Windows Time** foi reiniciado e seu estado foi consultado com `w32tm /query /status`.

A saída apresentada pelo laboratório, entretanto, reportou `Local CMOS Clock` como fonte atual, portanto ela não deve ser interpretada como comprovação de uma sincronização efetiva com `time.google.com` naquele momento.
