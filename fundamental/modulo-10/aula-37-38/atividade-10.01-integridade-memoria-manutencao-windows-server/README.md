# Atividade 10.1 — Integridade de Memória e Manutenção no Windows Server 2022

## Objetivo

Explorar os recursos de segurança **Memory Integrity**, **Core Isolation** e **Security and Maintenance** no Windows Server 2022, verificando também o histórico de confiabilidade e os recursos de manutenção automática do sistema.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Funções exploradas:** Windows Security e Security and Maintenance
* **Acesso:** RDP
* **Máquina:** Windows Server 2022 (cliente)

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao Windows Server 2022

O Windows Server 2022 (cliente) foi acessado via RDP.

Na tela de autenticação foi utilizado o usuário administrativo indicado no laboratório.

---

## 2. Acesso ao Device Security

Na barra de tarefas, foi selecionado:

```text id="w3q8mf"
Type here to search
```

Foi pesquisado:

```text id="c6r1yp"
Device security
```

e o recurso **Device security** foi aberto.

---

## 3. Verificação do Core Isolation

Na janela **Device security**, foi localizada a seção:

```text id="v9m2kd"
Core Isolation
```

O **Core Isolation** utiliza recursos de virtualização baseados em hardware para criar uma camada de isolamento para componentes críticos do sistema, especialmente processos relacionados ao kernel.

Esse mecanismo ajuda a reduzir a superfície de ataque e dificulta técnicas que procuram comprometer componentes de baixo nível do sistema operacional.

---

## 4. Acesso aos detalhes do Core Isolation

Foi selecionado o link:

```text id="p5x7ta"
Core isolation details
```

para visualizar as configurações disponíveis.

---

## 5. Verificação do Memory Integrity

Na página de detalhes foi localizada a opção:

```text id="h8n4zs"
Memory integrity
```

O recurso tem como objetivo proteger a integridade da memória do sistema, dificultando alterações indevidas no código executado em componentes protegidos do Windows.

---

## 6. Habilitação do Memory Integrity

O interruptor de **Memory integrity** estava em:

```text id="j2k6rw"
Off
```

Foi alterado para:

```text id="r7m3vc"
On
```

Com isso, o recurso foi habilitado.

---

## 7. Reinicialização do servidor

Após habilitar o recurso, o Windows apresentou um aviso informando que seria necessário reiniciar o sistema.

Na barra de tarefas foi utilizado:

```text id="n4p9yb"
Windows → Shut down or sign out → Restart → Continue
```

A máquina foi reiniciada e a conexão RDP foi perdida durante o processo.

---

## 8. Novo acesso após a reinicialização

Foi aguardado o período indicado pelo laboratório e realizado novamente o acesso ao Windows Server 2022 via RDP.

Após o acesso, foi verificado o estado do recurso **Memory integrity**.

> O material informa que, devido à natureza do gerenciamento da máquina virtual utilizada no laboratório, o recurso pode continuar aparecendo como `Off` mesmo após a tentativa de habilitação.

---

## 9. Acesso ao Security and Maintenance

Na barra de tarefas, foi pesquisado:

```text id="z5v8hx"
Security and Maintenance
```

O recurso foi aberto para explorar as opções de manutenção e confiabilidade do sistema.

---

## 10. Visualização do histórico de confiabilidade

Na janela **Security and Maintenance**, foi selecionado o texto:

```text id="q3n7wm"
Maintenance
```

Após expandir a seção, foi selecionado:

```text id="f6k2pa"
View reliability history
```

O **Reliability Monitor** permite consultar um histórico de eventos relacionados à estabilidade do sistema, incluindo falhas de aplicativos, problemas e outros eventos relevantes.

---

## 11. Visualização dos relatórios de problemas

Na janela do histórico de confiabilidade, foi selecionado:

```text id="m8r4yc"
View all problem reports
```

Essa opção permite consultar relatórios relacionados a problemas registrados no sistema, como falhas de aplicativos e outros eventos que podem afetar sua confiabilidade.

Após a visualização, foram selecionados **OK** nas janelas necessárias para retornar à tela anterior.

---

## 12. Configuração da manutenção automática

Novamente na seção:

```text id="Maintenance"
```

foi selecionada a opção:

```text id="t7w2nb"
Change Maintenance Settings
```

Essa configuração permite ajustar o agendamento da manutenção automática do Windows e definir o período em que essas atividades podem ser executadas.

Após visualizar as configurações, foi selecionado:

```text id="y4c9ks"
Cancel
```

para sair sem alterar as configurações.

---

## 13. Início da manutenção

Na seção **Maintenance**, foi selecionado:

```text id="a6p3vd"
Start maintenance
```

Essa opção inicia manualmente as atividades de manutenção disponíveis no sistema.

A ação pode envolver tarefas relacionadas à manutenção e à verificação do estado do sistema.

---

## Evidência — Passo 13

**Frase obrigatória antes do print:**

> **Print da atividade 10.1:** recurso `Start maintenance` da seção `Maintenance` do Windows Server 2022, demonstrando a opção de iniciar manualmente a manutenção do sistema.

[**Evidências — Módulo 10 / Aulas 37 e 38**](../evidencias.pdf)

---

## 14. Verificação da manutenção em andamento

Após iniciar a manutenção, foi verificado o aviso:

```text id="s8k5qx"
Maintenance in progress
```

Esse aviso indica que o processo de manutenção foi iniciado.

Após a verificação, as janelas foram fechadas.

---

## Fluxo da atividade

| Etapa                    | Resultado                                    |
| ------------------------ | -------------------------------------------- |
| Device Security          | Core Isolation e Memory Integrity explorados |
| Memory Integrity         | Habilitação e reinicialização realizadas     |
| Security and Maintenance | Recursos de manutenção explorados            |
| Start maintenance        | Processo de manutenção iniciado              |

## Resultado

Foram explorados os recursos de **Core Isolation**, **Memory Integrity** e **Security and Maintenance** do Windows Server 2022.

Também foi iniciado manualmente o processo de manutenção e verificado o estado **Maintenance in progress**.
