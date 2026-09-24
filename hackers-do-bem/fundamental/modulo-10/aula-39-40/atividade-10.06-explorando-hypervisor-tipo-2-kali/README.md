# Atividade 10.6 — Explorando um Hypervisor Tipo 2 no Kali Linux

## Objetivo

Explorar o **Oracle VM VirtualBox** no Kali Linux, identificando suas principais configurações e recursos disponíveis nas preferências do hypervisor.

O VirtualBox é um **Hypervisor Tipo 2**, pois é executado sobre um sistema operacional hospedeiro e permite criar e gerenciar máquinas virtuais.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Hypervisor:** Oracle VM VirtualBox
* **Acesso:** RDP
* **IP da VM:** `192.168.98.40`

---

## 1. Abrindo o VirtualBox

O acesso ao Kali Linux foi realizado via RDP.

Na barra de tarefas superior, foi acessado:

```text
Aplicativos
→ Aplicações habituais
→ Sistema
→ Oracle VM VirtualBox
```

Após a seleção, a janela principal do VirtualBox foi aberta.

---

## 2. Acessando as preferências

Na janela principal do VirtualBox, foi acessado:

```text
Arquivo → Preferências...
```

Uma nova janela contendo as configurações gerais do VirtualBox foi apresentada.

---

## 3. Verificando a pasta padrão das máquinas virtuais

Na aba **Geral**, foi verificada a opção **Pasta Padrão para Máquinas**.

O caminho apresentado foi:

```text
/home/aluno/VirtualBox VMs
```

Esse diretório é utilizado como local padrão para armazenamento das máquinas virtuais criadas pelo VirtualBox.

---

## 4. Verificando a biblioteca de autenticação VRDP

Ainda nas configurações gerais, foi observada a opção relacionada à **Biblioteca de Autenticação VRDP**.

O VRDP (**VirtualBox Remote Desktop Protocol**) é utilizado para permitir conexões remotas com máquinas virtuais do VirtualBox.

A opção padrão apresentada no laboratório foi:

```text
VBoxAuth
```

---

## 5. Explorando as configurações de entrada

Na coluna esquerda das preferências, foi selecionada a opção:

```text
Entrada
```

Na aba referente ao **Gerenciador do VirtualBox**, foram observados os comandos disponíveis para gerenciamento do VirtualBox e seus respectivos atalhos de teclado.

Em seguida, foi selecionada a opção:

```text
Máquina Virtual
```

Nessa seção foram observados os comandos e atalhos relacionados ao gerenciamento das máquinas virtuais.

---

## 6. Acessando as configurações de idioma

Na coluna esquerda das preferências, foi selecionada:

```text
Idioma
```

Na área direita foram apresentados os idiomas disponíveis para a interface do VirtualBox.

A opção utilizada estava configurada como:

```text
Padrão
```

Nesse modo, o VirtualBox utiliza o idioma definido pelo sistema operacional hospedeiro. Como o Kali Linux utilizado no laboratório estava em português, a interface do VirtualBox também foi apresentada em português.

---

## Evidência — Passo 7

**Frase obrigatória antes do print:**

> **Print da atividade 10.6:** tela de configurações de idioma do Oracle VM VirtualBox, exibindo os idiomas disponíveis e a opção padrão selecionada.

[**Evidências — Módulo 10 / Aulas 39 e 40**](../evidencias.pdf)

---

## 7. Explorando as configurações de tela

Após a verificação do idioma, foi selecionada a opção:

```text
Tela
```

Foram observadas as configurações disponíveis para a interface gráfica, incluindo:

* Tamanho Máximo da Tela do Sistema Convidado;
* Fator de Escalonamento;
* Recursos Estendidos;
* Escalonamento de Fontes.

Essas opções permitem ajustar aspectos relacionados à exibição das máquinas virtuais e da interface gráfica.

---

## 8. Encerrando as preferências

Após a exploração das configurações, foi selecionado:

```text
OK
```

A janela **VirtualBox - Preferências** foi fechada.

O VirtualBox permaneceu aberto para continuidade da atividade seguinte.

---

## Conceitos

* **Hypervisor Tipo 2:** software de virtualização executado sobre um sistema operacional hospedeiro.
* **VirtualBox:** plataforma utilizada para criar e gerenciar máquinas virtuais.
* **VRDP:** protocolo utilizado pelo VirtualBox para acesso remoto a máquinas virtuais.
* **Preferências:** conjunto de configurações gerais utilizadas pelo VirtualBox.

## Fluxo da atividade

```text
Abrir VirtualBox
      ↓
Acessar Preferências
      ↓
Explorar configurações
      ↓
Verificar Entrada
      ↓
Verificar Máquina Virtual
      ↓
Verificar Idioma
      ↓
Verificar Tela
      ↓
Fechar Preferências
```

## Resultado

Foram exploradas as principais configurações das preferências do VirtualBox, incluindo armazenamento, autenticação VRDP, atalhos, idioma e ajustes de tela.
