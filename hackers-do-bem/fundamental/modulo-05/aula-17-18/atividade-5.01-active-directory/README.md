# Atividade 5.1 — Criando o Active Directory no Windows Server 2022

## Objetivo

Instalar e preparar o **Active Directory Domain Services (AD DS)** no Windows Server 2022, configurando o servidor que posteriormente será promovido a **Domain Controller**.

Nesta etapa também são instaladas as funções relacionadas ao **DNS** e aos recursos de gerenciamento necessários para as próximas atividades.

---

## Ambiente

* Windows Server 2022
* Server Manager
* Active Directory Domain Services (AD DS)
* DNS Server
* Group Policy Management
* Remote Server Administration Tools

---

## 1. Acesso ao Windows Server 2022

O Windows Server 2022 utilizado no laboratório foi acessado por RDP.

```text
IP: 192.168.98.20
Usuário: Administrator
```

As credenciais utilizadas para acesso pertencem ao ambiente do laboratório e não são registradas neste documento.

Após a conexão, foi aberto o **Server Manager**.

---

## 2. Alterando o nome do servidor

No **Server Manager**, foi acessado:

```text
Local Server
```

Em seguida, foi selecionado o nome atual do computador e aberta a opção:

```text
Change...
```

O nome do computador foi alterado para:

```text
DC01
```

Após confirmar a alteração, o Windows Server foi reiniciado para aplicar o novo nome.

Depois da reinicialização, o **Server Manager** foi aberto novamente para confirmar a alteração.

---

## 3. Adicionando as funções do servidor

No canto superior direito do **Server Manager**, foi acessado:

```text
Manage
    ↓
Add Roles and Features
```

O assistente de instalação foi iniciado.

Foi avançado pelas etapas iniciais até chegar à tela:

```text
Server Roles
```

---

## 4. Instalando o Active Directory Domain Services

Na tela **Server Roles**, foi selecionada a função:

```text
Active Directory Domain Services
```

Ao aparecer a janela solicitando recursos adicionais, foi selecionado:

```text
Add Features
```

Essa função fornece os componentes necessários para posteriormente configurar o servidor como controlador de domínio.

---

## 5. Instalando o DNS Server

Ainda na seleção de funções, foi ativada a opção:

```text
DNS Server
```

Em seguida, foi selecionado:

```text
Add Features
```

Foi confirmada a janela apresentada e o assistente continuou para as próximas etapas.

---

## 6. Verificando os recursos adicionais

Na tela **Features**, foram verificadas as opções relacionadas ao gerenciamento do servidor.

Entre elas estavam:

```text
Group Policy Management
Remote Server Administration Tools
```

Esses componentes serão utilizados posteriormente para administração do domínio e das políticas do Active Directory.

O assistente foi avançado até a etapa:

```text
Confirmation
```

---

## 7. Instalando as funções

Na tela **Confirmation**, foram verificadas as funções selecionadas.

A instalação foi iniciada através do botão:

```text
Install
```

A evidência solicitada pelo laboratório corresponde a esta etapa.

Após o início da instalação, o assistente apresentou a barra de progresso da instalação das funções.

---

## Conceitos

### Active Directory Domain Services (AD DS)

O **Active Directory Domain Services** é o serviço de diretório do Windows Server utilizado para organizar e administrar recursos de uma rede baseada em domínio.

Ele permite centralizar informações relacionadas a:

* usuários;
* computadores;
* grupos;
* autenticação;
* permissões;
* políticas de segurança.

Nesta atividade, o AD DS foi instalado, mas o servidor ainda será promovido a **Domain Controller** na atividade 5.2.

### Domain Controller

Um **Domain Controller (DC)** é um servidor que executa os serviços necessários para autenticar usuários e administrar um domínio do Active Directory.

A instalação do AD DS é uma etapa necessária antes da promoção do servidor a Domain Controller.

### DNS

O **Domain Name System (DNS)** traduz nomes de domínio em informações utilizadas pelos dispositivos da rede.

No Active Directory, o DNS possui papel fundamental na localização dos serviços do domínio. Por isso, a função **DNS Server** também foi instalada durante esta atividade.

### Group Policy Management

O **Group Policy Management** fornece ferramentas para criação e administração de **Group Policy Objects (GPOs)**.

As GPOs serão utilizadas posteriormente no laboratório para aplicar configurações de segurança e políticas aos usuários e computadores do domínio.

---

## Resultado

O Windows Server 2022 foi preparado para funcionar como infraestrutura de Active Directory.

Foram instaladas as funções:

```text
Active Directory Domain Services
DNS Server
```

Além dos recursos de gerenciamento necessários para as próximas etapas.

O servidor foi identificado como:

```text
DC01
```

A próxima atividade utilizará essa instalação para promover o servidor a **Domain Controller** e criar uma nova floresta do Active Directory.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 1 e 2**](../evidencias.pdf)

**Evidência registrada:** passo 9 — tela **Confirmation** do assistente de instalação, antes da instalação das funções do servidor.
