# Atividade 12.1 — Explorando os Logs no Windows Server 2022

## Objetivo

Explorar os principais registros de eventos disponíveis no **Windows Server 2022** através do **Event Viewer (Visualizador de Eventos)**, identificando diferentes categorias de logs e utilizando o filtro de eventos para restringir a visualização dos registros.

---

## Ambiente

* **Sistema operacional:** Windows Server 2022
* **Acesso:** RDP
* **Ferramenta:** Event Viewer (`eventvwr.msc`)
* **Logs analisados:** Application, Security, Setup, System e Forwarded Events

---

## 1. Acessando o Event Viewer

O Windows Server 2022 foi inicializado e acessado através de RDP.

No campo de pesquisa da barra de tarefas, foi digitado:

```text id="w3r8kp"
eventvwr.msc
```

Em seguida, foi aberto o aplicativo **Event Viewer**.

---

## 2. Explorando os Windows Logs

No painel esquerdo do Event Viewer, foi expandida a opção:

```text
Windows Logs
```

Essa seção reúne diferentes categorias de eventos registrados pelo sistema operacional.

Os principais logs disponíveis são:

### Application

Registra eventos gerados por aplicativos e programas em execução no sistema, incluindo informações, avisos e erros relacionados ao funcionamento dos softwares.

### Security

Registra eventos relacionados à segurança do sistema, como autenticações, tentativas de acesso, alterações de políticas e atividades relacionadas às contas de usuário.

### Setup

Registra eventos relacionados à instalação e configuração de componentes do sistema operacional e de softwares.

### System

Registra eventos gerados pelo próprio sistema operacional, incluindo informações sobre inicialização, drivers, hardware e componentes do sistema.

### Forwarded Events

Permite centralizar eventos encaminhados por outros computadores da rede, sendo útil para ambientes que utilizam coleta centralizada de logs.

---

## 3. Explorando o log Application

Dentro de:

```text
Windows Logs → Application
```

foi observado o histórico dos eventos de aplicação registrados no servidor.

Em seguida, foi aberto o primeiro evento disponível na lista.

A janela de detalhes apresenta informações como:

* **Log Name:** categoria do log em que o evento foi registrado.
* **Source:** componente ou aplicativo responsável pela geração do evento.
* **Event ID:** identificador numérico do evento.
* **Level:** nível do evento, como informação, aviso ou erro.
* **User:** usuário associado ao evento.
* **OpCode:** código que identifica a operação relacionada ao evento.
* **Logged:** data e hora em que o evento foi registrado.
* **Task Category:** categoria específica da tarefa relacionada ao evento.
* **Computer:** computador responsável pela geração do evento.

Essas informações são importantes para analisar o contexto de um evento e identificar sua origem, gravidade e momento de ocorrência.

Após a análise, a janela do evento foi fechada.

---

## 4. Explorando os demais logs

Ainda dentro de:

```text
Windows Logs
```

foram acessadas as seguintes categorias:

### Security

Foi visualizado o histórico de eventos relacionados à segurança do Windows Server.

Esses registros podem ser utilizados, por exemplo, para investigar autenticações, alterações de contas e outros eventos de segurança.

### Setup

Foi visualizado o histórico de eventos relacionados à instalação e configuração do sistema.

### System

Foi visualizado o histórico de eventos gerados pelo sistema operacional, incluindo informações relacionadas a serviços, drivers e funcionamento do sistema.

### Forwarded Events

Foi visualizado o histórico destinado a eventos encaminhados de outros computadores.

---

## 5. Acessando o filtro do log Application

Após retornar para:

```text
Windows Logs → Application
```

foi acessado o painel **Actions**, localizado à direita.

Em seguida, foi selecionada a opção:

```text
Filter Current Log...
```

Essa funcionalidade permite restringir os eventos apresentados no log de acordo com diferentes critérios.

---

## 6. Explorando os parâmetros de filtragem

A janela **Filter Current Log** apresenta diversos parâmetros que podem ser utilizados para filtrar os eventos.

### Logged

Permite definir um intervalo de datas e horários para os eventos que serão exibidos.

É possível, por exemplo, restringir a pesquisa a eventos registrados em determinado período.

### Event logs

Permite selecionar quais logs serão considerados pelo filtro.

Nesse caso, o log **Application** aparece selecionado por padrão.

### Event sources

Permite selecionar as fontes responsáveis pela geração dos eventos.

Isso possibilita concentrar a análise em determinado aplicativo ou componente do sistema.

### Task category

Permite utilizar a categoria da tarefa como critério de filtragem.

No contexto apresentado pelo laboratório, esse campo não pode ser editado.

### Keywords

Permite utilizar palavras-chave associadas aos eventos para restringir os resultados.

Essas palavras-chave podem ajudar a identificar determinados tipos de eventos, como informações relacionadas a erros ou segurança.

### Users

Permite filtrar eventos relacionados a usuários específicos.

Esse recurso pode ser útil para investigar atividades associadas a determinada conta.

### Computer(s)

Permite selecionar o computador associado aos eventos.

Em ambientes com múltiplos computadores e coleta centralizada de eventos, esse filtro pode ajudar a restringir a análise a uma máquina específica.

---

## 7. Evidência

O print obrigatório da atividade corresponde ao **passo 10**, mostrando a janela **Filter Current Log** aberta sobre o log **Application**, com os parâmetros disponíveis para filtragem.

**Frase obrigatória antes do print:**

> **Print da atividade 12.1:** janela `Filter Current Log` do Event Viewer, exibindo os parâmetros disponíveis para filtragem dos eventos do log `Application` no Windows Server 2022.

[**Evidências — Módulo 12 / Aulas 45 e 46**](../evidencias.pdf)

---

## 8. Encerramento

Após a exploração dos logs e da ferramenta de filtragem, todas as janelas foram fechadas, mantendo a conexão RDP ativa para continuidade da atividade seguinte.

---

## Conceitos

* **Event Viewer:** ferramenta do Windows utilizada para visualizar e analisar eventos registrados pelo sistema.
* **Windows Logs:** conjunto de categorias de eventos do Windows, como Application, Security, Setup, System e Forwarded Events.
* **Event ID:** identificador utilizado para diferenciar tipos de eventos.
* **Event Source:** componente responsável pela geração do evento.
* **Log Level:** indica a categoria ou gravidade do evento, como informação, aviso ou erro.
* **Event filtering:** permite restringir os eventos exibidos de acordo com critérios específicos.

## Fluxo

```text
Windows Server 2022
        ↓
Event Viewer
        ↓
Windows Logs
        ↓
Application / Security / Setup
System / Forwarded Events
        ↓
Filter Current Log
        ↓
Análise dos critérios de filtragem
```

## Resultado

Foi realizada a exploração dos principais logs do Windows Server 2022 e dos detalhes associados aos eventos registrados. Também foi utilizada a funcionalidade **Filter Current Log** para identificar os diferentes critérios disponíveis para filtrar eventos do sistema.
