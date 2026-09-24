# Atividade 11.5 — QoS no Windows Server 2022

## Objetivo

Configurar uma política de **Quality of Service (QoS)** no Windows Server 2022 utilizando o **Editor de Política de Grupo Local**, definindo um limite de taxa de saída e verificando o impacto da configuração por meio de um teste de velocidade.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Acesso:** RDP
* **Ferramenta:** Editor de Política de Grupo Local
* **Configuração:** Policy-based QoS
* **Nome da política:** `Teste`
* **Limite configurado:** `1 MBps`

> A configuração de `1 MBps` corresponde aproximadamente a `8 Mbps`, considerando a conversão entre bytes e bits.

---

## 1. Realizando o teste inicial de velocidade

O Windows Server 2022 foi acessado através de RDP.

Inicialmente, foi aberto o navegador Microsoft Edge e acessado o site:

```text
https://www.minhaconexao.com.br/
```

Foi realizado um teste de velocidade para estabelecer uma referência antes da configuração de QoS.

No teste inicial, a velocidade de **upload estava acima de 20 Mbps**.

Após o teste, o navegador foi fechado.

---

## 2. Abrindo o Editor de Política de Grupo Local

Foi utilizado o menu de pesquisa do Windows para localizar:

```text
gpedit.msc
```

O **Editor de Política de Grupo Local** foi aberto.

---

## 3. Acessando as configurações de QoS

No Editor de Política de Grupo Local, foi acessado o seguinte caminho:

```text
Configuração do Computador
└── Configurações do Windows
    └── Policy-based QoS
```

Na opção **Policy-based QoS**, foi utilizado o botão direito do mouse e selecionado:

```text
Create new policy
```

---

## 4. Criando a política

Foi iniciado o assistente de criação de uma nova política de QoS.

No campo de nome da política, foi definido:

```text
Teste
```

A política foi criada com esse nome para facilitar sua identificação posteriormente.

---

## 5. Configurando o valor DSCP

Na etapa de configuração do DSCP, foi mantido o valor:

```text
0
```

O DSCP (*Differentiated Services Code Point*) é utilizado para marcar pacotes de acordo com diferentes classes de serviço.

Neste laboratório, não foi aplicada uma marcação DSCP específica.

---

## 6. Ativando o limite de saída

Na etapa seguinte, foi habilitada a opção:

```text
Specify Outbound Throttle Rate
```

Foi definido o valor:

```text
1 MBps
```

Essa configuração estabelece uma limitação para a taxa de tráfego de saída associada à política.

Como referência:

```text
1 Byte = 8 bits
1 MB/s ≈ 8 Mb/s
```

Portanto, o limite configurado representa aproximadamente **8 Mbps** quando convertido para megabits por segundo.

---

## 7. Definindo os aplicativos

Na etapa de seleção dos aplicativos, foi escolhida a opção:

```text
All applications
```

Dessa forma, a política não ficou restrita a um aplicativo específico.

---

## 8. Definindo o endereço IP de origem

Na configuração dos endereços IP de origem, foi selecionada:

```text
Any source IP address
```

Assim, a política pode ser aplicada independentemente do endereço IP de origem.

---

## 9. Definindo as portas

Na configuração das portas, foram mantidas as opções:

```text
From any source port
To any destination port
```

A política, portanto, não foi limitada a uma porta de origem ou destino específica.

---

## 10. Finalizando a política

Após revisar as configurações, o assistente foi finalizado.

A política criada possui as seguintes características:

| Configuração     | Valor    |
| ---------------- | -------- |
| Nome             | `Teste`  |
| DSCP             | `0`      |
| Limite de saída  | `1 MBps` |
| Aplicativos      | Todos    |
| IP de origem     | Qualquer |
| Porta de origem  | Qualquer |
| Porta de destino | Qualquer |

---

## 11. Verificando a política criada

No **Editor de Política de Grupo Local**, foi acessado novamente:

```text
Configuração do Computador
→ Configurações do Windows
→ Policy-based QoS
```

A política `Teste` foi exibida na lista de políticas configuradas.

---

## 12. Realizando novamente o teste de velocidade

O Microsoft Edge foi aberto novamente e o site abaixo foi acessado:

```text
https://www.minhaconexao.com.br/
```

Foi realizado um novo teste de velocidade para verificar o comportamento da conexão após a aplicação da política.

---

## 13. Comparando com o teste inicial

No primeiro teste, realizado antes da política, o upload estava acima de **20 Mbps**.

Após a configuração da política `Teste`, o upload observado ficou aproximadamente na faixa de:

```text
7–10 Mbps
```

Essa redução é compatível com o objetivo do laboratório de aplicar um limite de tráfego de aproximadamente `1 MBps`, embora o resultado efetivo do teste possa variar conforme as condições da conexão e do próprio servidor de teste.

---

## 14. Evidência do teste de velocidade

O teste de velocidade foi realizado novamente após a configuração da política de QoS.

### Evidência — Passo 14

**Frase obrigatória antes do print:**

> **Print da atividade 11.5:** teste de velocidade realizado após a criação da política de QoS `Teste`, mostrando o comportamento da velocidade de upload após a aplicação do limite de tráfego configurado.

[**Evidências — Módulo 11 / Aulas 41 e 42**](../evidencias.pdf)

---

## 15. Removendo a política de QoS

Após o registro da evidência, o navegador foi fechado.

No **Editor de Política de Grupo Local**, a política `Teste` foi localizada em:

```text
Configuração do Computador
→ Configurações do Windows
→ Policy-based QoS
```

A política foi selecionada com o botão direito e removida através da opção:

```text
Delete
```

A confirmação foi realizada selecionando:

```text
Yes
```

Com isso, a política de limitação criada durante o laboratório foi removida.

---

## Conceitos

* **QoS:** mecanismo utilizado para controlar e organizar o tráfego de rede.
* **Policy-based QoS:** permite aplicar políticas de controle de tráfego por meio das políticas do Windows.
* **DSCP:** campo utilizado para classificação de tráfego IP.
* **Outbound Throttle:** mecanismo de limitação da taxa de tráfego de saída.
* **Mbps:** megabits por segundo.
* **MBps/MB/s:** megabytes por segundo.

## Fluxo da atividade

```text
Teste de velocidade inicial
          ↓
Abrir gpedit.msc
          ↓
Policy-based QoS
          ↓
Criar política "Teste"
          ↓
DSCP = 0
          ↓
Limite = 1 MBps
          ↓
Aplicar a todos os aplicativos
          ↓
Qualquer IP e qualquer porta
          ↓
Novo teste de velocidade
          ↓
Comparar resultados
          ↓
Remover política
```

## Resultado

Foi criada uma política **Policy-based QoS** chamada `Teste`, configurada para limitar o tráfego de saída a `1 MBps`. Após sua aplicação, o teste de velocidade apresentou upload na faixa de **7–10 Mbps**, em comparação com mais de **20 Mbps** no teste inicial. Ao final, a política foi removida.
