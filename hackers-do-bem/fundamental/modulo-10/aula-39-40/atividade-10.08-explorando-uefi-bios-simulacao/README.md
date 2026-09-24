# Atividade 10.8 — Explorando uma UEFI/BIOS por Simulação

## Objetivo

Explorar uma interface **UEFI/BIOS simulada** disponibilizada pela Lenovo, identificando informações do sistema e as principais configurações relacionadas a hardware, segurança e inicialização.

---

## Ambiente

* **Sistema:** computador pessoal
* **Navegador:** Mozilla Firefox
* **Recurso:** Lenovo UEFI/BIOS Simulator
* **Modelo simulado:** Lenovo Slim Pro 9 16IRP8 (83C0)
* **Interface:** Graphics Interface Mode

---

## 1. Acessando o simulador de UEFI/BIOS

A atividade foi realizada no computador pessoal, conforme orientação do laboratório, sem utilizar a VM da AWS.

No navegador, foi acessado:

```text id="qk0x1x"
https://download.lenovo.com/bsco/index.html#/
```

O recurso disponibilizado pela Lenovo permite simular a interface de configuração de diferentes equipamentos.

---

## 2. Iniciando o simulador

Na página inicial do recurso, foi selecionado:

```text id="nqj1kg"
Launch Simulator
```

Em seguida, foi selecionada a categoria:

```text id="1q3q7e"
Laptops
```

Depois:

```text id="x9f4d2k"
Lenovo Laptops
```

---

## 3. Selecionando o equipamento

Na lista de equipamentos disponíveis, foi selecionado:

```text id="l8h3zw"
Lenovo Slim Pro 9 16IRP8 (83C0)
```

Em seguida, foi escolhida a opção:

```text id="u5w8pn"
Graphics Interface Mode
```

A interface da UEFI/BIOS foi então inicializada de forma simulada.

---

## 4. Explorando a seção Information

Na tela inicial da BIOS simulada, foi observada a seção:

```text id="3o2q7m"
Information
```

Nessa área são apresentadas informações relacionadas ao equipamento, incluindo:

* Nome do produto;
* Versão da BIOS;
* CPU;
* Memória do sistema;
* Secure Boot.

Essas informações permitem consultar características básicas do equipamento diretamente pela interface de firmware.

---

## 5. Explorando a seção Configuration

Na coluna esquerda, foi selecionada:

```text id="8d0z4r"
Configuration
```

Foram observadas configurações relacionadas ao funcionamento do equipamento, incluindo:

* Time;
* Date;
* WLAN;
* Graphics Device;
* Intel(R) Virtualization Technology;
* Always On USB;
* Charge in Battery Mode;
* System Performance Mode.

A seção **Configuration** reúne opções relacionadas ao comportamento e aos recursos de hardware do equipamento.

---

## 6. Explorando a seção Security

Em seguida, foi selecionada:

```text id="n7s2x1"
Security
```

Foram observadas configurações de segurança da UEFI/BIOS, entre elas:

* Set Hard Disk Password;
* Intel Platform Trust Technology;
* Device Guard;
* Secure Boot;
* Reset to Setup Mode;
* Restore Factory Keys.

Essas opções demonstram como a UEFI/BIOS pode participar de mecanismos relacionados à proteção do dispositivo, inicialização segura e confiança da plataforma.

---

## 7. Explorando a seção Boot

Na coluna esquerda, foi selecionada:

```text id="0x4k8p"
Boot
```

Foram observadas as opções relacionadas ao processo de inicialização do equipamento, incluindo:

* USB Boot;
* PXE Boot to LAN;
* IPV4 PXE First;
* EFI;
* Windows Boot Manager;
* EFI PXE Network.

A seção **Boot** permite consultar e configurar diferentes mecanismos e fontes utilizadas durante a inicialização do sistema.

---

## Evidência — Passo 8

**Frase obrigatória antes do print:**

> **Print da atividade 10.8:** tela `Boot` da UEFI/BIOS simulada do Lenovo Slim Pro 9 16IRP8 (83C0), exibindo as configurações relacionadas ao processo de inicialização.

[**Evidências — Módulo 10 / Aulas 39 e 40**](../evidencias.pdf)

---

## 8. Saindo da UEFI/BIOS simulada

Após concluir a exploração das configurações, foi acessado:

```text id="5r7m2v"
Exit → Exit Discarding Changes
```

Foi selecionado:

```text id="4e9n1c"
Yes
```

A opção **Exit Discarding Changes** permite sair do simulador sem salvar eventuais alterações realizadas durante a exploração.

Por fim, o navegador foi fechado.

---

## Conceitos

* **UEFI:** firmware moderno responsável pela inicialização e configuração de recursos do computador.
* **BIOS:** firmware tradicional utilizado para inicializar e configurar o hardware.
* **Secure Boot:** mecanismo que ajuda a verificar componentes autorizados durante a inicialização.
* **Boot:** processo de inicialização do sistema e seleção das fontes de inicialização.
* **PXE:** mecanismo que permite inicialização pela rede.

## Fluxo da atividade

```text id="4l6k8s"
Acessar simulador
      ↓
Launch Simulator
      ↓
Selecionar Laptop
      ↓
Selecionar modelo
      ↓
Explorar Information
      ↓
Explorar Configuration
      ↓
Explorar Security
      ↓
Explorar Boot
      ↓
Exit Discarding Changes
```

## Resultado

Foi explorada uma UEFI/BIOS simulada, identificando informações do equipamento e configurações de **hardware, segurança e inicialização** sem necessidade de alterar o firmware real do computador.
