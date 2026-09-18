# Atividade 10.3 — Explorando as Atualizações no Windows Server 2022

## Objetivo

Explorar o ambiente de atualizações do Windows Server 2022, verificando a disponibilidade de atualizações, realizando a atualização do sistema e analisando as opções avançadas de atualização e notificações.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Recurso:** Windows Update
* **Acesso:** RDP
* **Máquina:** Windows Server 2022 (cliente)

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao Windows Server 2022

O Windows Server 2022 (cliente) foi acessado via RDP utilizando as credenciais administrativas indicadas no laboratório.

---

## 2. Acesso ao Windows Update

Na barra de tarefas, foi selecionado:

```text id="q7m3va"
Type here to search
```

Foi pesquisado:

```text id="x4p8kc"
Windows Update settings
```

e o recurso foi aberto.

---

## 3. Verificação de atualizações

Na página do Windows Update, foi selecionado o botão:

```text id="h6w2ry"
Check for updates
```

O sistema iniciou a verificação de atualizações disponíveis.

Conforme orientado pelo laboratório, foi aguardado o término do processo para permitir que as atualizações encontradas fossem baixadas e instaladas.

---

## 4. Reinicialização do Windows Server

Ao final do processo de atualização, o sistema apresentou a opção:

```text id="p9c5tb"
Restart Now
```

A reinicialização foi realizada.

Como consequência, a conexão RDP foi encerrada temporariamente.

Foi aguardado o período indicado no laboratório e realizado novamente o acesso ao Windows Server 2022.

Após a reconexão, foi acessado novamente:

```text id="Windows Update settings"
```

---

## 5. Verificação do estado das atualizações

Após o processo de atualização e reinicialização, foi verificada a mensagem:

```text id="a3n8xf"
You're up to date
```

Essa mensagem indica que, naquele momento, o Windows Update não apresentava novas atualizações pendentes para instalação.

---

## 6. Configuração das opções avançadas

Foi selecionado:

```text id="m5v7qd"
Advanced options
```

Na seção **Update options** e em **Update notifications**, foram ativadas as opções disponíveis conforme solicitado no laboratório.

Após a configuração, foi utilizada a seta de retorno localizada no canto superior esquerdo para voltar à página anterior.

---

## Evidência — Passo 6

**Frase obrigatória antes do print:**

> **Print da atividade 10.3:** tela de configurações avançadas do Windows Update após a ativação das opções de atualização e notificações solicitadas no laboratório.

[**Evidências — Módulo 10 / Aulas 37 e 38**](../evidencias.pdf)

---

## 7. Visualização do histórico de atualizações

Na página principal do Windows Update, foi selecionada a opção:

```text id="v8k2ws"
View update history
```

Essa área permite consultar as atualizações instaladas anteriormente no sistema, incluindo informações relacionadas ao histórico de instalação.

---

## 8. Encerramento

Após a visualização do histórico de atualizações, todas as janelas foram fechadas.

---

## Fluxo da atividade

| Etapa             | Resultado                                         |
| ----------------- | ------------------------------------------------- |
| Windows Update    | Ambiente acessado                                 |
| Check for updates | Atualizações verificadas                          |
| Reinicialização   | Sistema reiniciado após atualização               |
| Advanced options  | Opções de atualização e notificações configuradas |
| Update history    | Histórico consultado                              |

## Resultado

O ambiente do **Windows Update** foi explorado no Windows Server 2022, incluindo a verificação e instalação de atualizações.

Também foram analisadas as opções avançadas de atualização e notificações e o histórico de atualizações do sistema.
