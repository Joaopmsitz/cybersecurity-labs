# Atividade 10.2 — Controle de Aplicativos e Navegadores no Windows Server 2022

## Objetivo

Explorar os recursos de **App & browser control**, **Reputation-based protection** e **Exploit Protection** do Windows Security no Windows Server 2022, verificando as principais configurações de proteção contra aplicativos maliciosos e técnicas de exploração.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Ferramenta:** Windows Security
* **Recursos:** App & browser control, Reputation-based protection e Exploit Protection
* **Acesso:** RDP
* **Máquina:** Windows Server 2022 (cliente)

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao Windows Server 2022

O Windows Server 2022 (cliente) foi acessado via RDP utilizando as credenciais administrativas indicadas no laboratório.

---

## 2. Acesso ao App & browser control

Na barra de tarefas, foi selecionado:

```text id="x6m2qp"
Type here to search
```

Foi pesquisado:

```text id="r8v4kc"
App & browser control
```

e o recurso foi aberto.

---

## 3. Verificação do Reputation-based protection

Na janela **App & browser control**, foi localizada a seção:

```text id="h5n9wb"
Reputation-based protection
```

No estado inicial observado durante a atividade, a funcionalidade estava desabilitada e apresentava a opção:

```text id="p3c7yf"
Turn on
```

A proteção baseada em reputação utiliza informações sobre arquivos, aplicativos e suas origens para ajudar a identificar conteúdos potencialmente maliciosos.

---

## 4. Acesso às configurações de proteção baseada em reputação

Foi selecionado o link:

```text id="v2k8sd"
Reputation-based protection settings
```

para visualizar as configurações disponíveis.

---

## 5. Verificação do Check apps and files

Na tela de configurações, foi localizada a opção:

```text id="m7q4xa"
Check apps and files
```

Essa configuração permite verificar aplicativos e arquivos com base em informações de reputação, ajudando a identificar conteúdos potencialmente perigosos antes de sua execução ou abertura.

---

## 6. Habilitação do Potentially unwanted app blocking

Foi localizada a opção:

```text id="Potentially unwanted app blocking"
```

O recurso estava inicialmente em:

```text id="Off"
```

e foi alterado para:

```text id="On"
```

Esse mecanismo ajuda a bloquear aplicativos potencialmente indesejados, que podem apresentar comportamentos indesejáveis mesmo sem necessariamente serem classificados como malware tradicional.

---

## 7. Retorno à página anterior

Foi utilizado o botão de retorno localizado no canto superior esquerdo para retornar à página principal de:

```text id="App & browser control"
```

---

## 8. Verificação do Reputation-based protection

Após a alteração realizada anteriormente, foi verificado que o recurso:

```text id="Reputation-based protection"
```

passou a aparecer como habilitado.

---

## 9. Acesso ao Exploit Protection

Na página **App & browser control**, foi localizada a seção:

```text id="Exploit Protection"
```

O **Exploit Protection** fornece mecanismos de mitigação destinados a dificultar técnicas de exploração de vulnerabilidades em aplicativos e no próprio sistema operacional.

Foi selecionado o link:

```text id="Exploit protection settings"
```

---

## 10. Verificação das proteções de sistema

Na tela **Exploit protection**, foi acessada a aba:

```text id="System settings"
```

Foram observadas diversas proteções de sistema habilitadas por padrão.

Entre elas:

### Control Flow Guard (CFG)

O **Control Flow Guard** ajuda a proteger aplicações contra técnicas que tentam alterar ou desviar o fluxo normal de execução do programa.

### Data Execution Prevention (DEP)

O **Data Execution Prevention** ajuda a impedir a execução de código em determinadas regiões de memória destinadas a dados, reduzindo o impacto de algumas técnicas de exploração.

### Force randomization for images (Mandatory ASLR)

Essa configuração utiliza **ASLR (Address Space Layout Randomization)** para dificultar a previsão dos endereços de memória utilizados por módulos de programas.

### Randomize memory allocations (Bottom-up ASLR)

Realiza a aleatorização das alocações de memória, dificultando que um atacante dependa de endereços previsíveis durante uma exploração.

### High-entropy ASLR

Amplia a quantidade de aleatoriedade utilizada na disposição dos endereços de memória, aumentando a dificuldade de previsibilidade em determinados ambientes.

### Validate exception chains (SEHOP)

O **SEHOP (Structured Exception Handling Overwrite Protection)** ajuda a validar as cadeias de tratamento de exceções, dificultando determinadas técnicas de exploração baseadas em corrupção dessas estruturas.

### Validate heap integrity

Realiza verificações relacionadas à integridade das estruturas do heap, ajudando a detectar condições associadas à corrupção de memória.

---

## Evidência — Passo 10

**Frase obrigatória antes do print:**

> **Print da atividade 10.2:** tela `Exploit protection settings`, na aba `System settings`, apresentando as configurações de proteção contra técnicas de exploração do Windows Server 2022.

[**Evidências — Módulo 10 / Aulas 37 e 38**](../evidencias.pdf)

---

## 11. Encerramento

Após a visualização das configurações, todas as janelas foram fechadas.

---

## Fluxo da atividade

| Etapa                       | Resultado                           |
| --------------------------- | ----------------------------------- |
| App & browser control       | Recurso explorado                   |
| Reputation-based protection | Configurações verificadas           |
| PUA Blocking                | Habilitado                          |
| Exploit Protection          | Configurações de sistema analisadas |

## Resultado

Foram explorados os mecanismos de proteção de aplicativos e navegadores do Windows Security.

Também foram analisadas as principais mitigações do **Exploit Protection**, incluindo CFG, DEP, ASLR, SEHOP e validação da integridade do heap.
