# Atividade 2.10 — Políticas de Segurança Local no Windows Server 2022

## Objetivo

Explorar as **Políticas de Segurança Local** do Windows Server 2022, identificando configurações relacionadas ao gerenciamento de contas, senhas, bloqueio de contas, auditoria, atribuição de direitos de usuário e opções de segurança.

A atividade demonstra como essas políticas podem ser utilizadas para estabelecer controles de segurança e registrar determinadas ações realizadas no sistema.

## Ambiente

* Windows Server 2022
* Local Security Policy
* `secpol.msc`
* Account Policies
* Local Policies
* Audit Policy
* User Rights Assignment
* Security Options

## 1. Abrindo a Política de Segurança Local

No Windows Server 2022, foi realizada uma busca por:

```text
secpol
```

Em seguida, foi aberta a ferramenta:

```text
Local Security Policy
```

A ferramenta permite visualizar e administrar diversas configurações de segurança do sistema operacional.

## 2. Account Policies

Dentro de **Local Security Policy**, foi acessado:

```text
Account Policies
```

Essa categoria contém configurações relacionadas ao gerenciamento de contas e autenticação.

### Password Policy

Dentro de:

```text
Account Policies → Password Policy
```

foram observadas as seguintes políticas:

* Enforce password history
* Maximum password age
* Minimum password age
* Minimum password length
* Password must meet complexity requirements

Essas configurações permitem estabelecer requisitos para a criação e manutenção das senhas dos usuários.

### Enforce password history

Define a quantidade de senhas anteriores que podem ser lembradas pelo sistema, dificultando a reutilização imediata de credenciais antigas.

### Maximum password age

Define por quanto tempo uma senha pode permanecer válida antes de precisar ser alterada.

### Minimum password age

Determina o período mínimo durante o qual uma senha deve permanecer válida antes que possa ser alterada novamente.

### Minimum password length

Define a quantidade mínima de caracteres exigida para uma senha.

### Password must meet complexity requirements

Permite exigir que as senhas atendam aos requisitos de complexidade definidos pelo Windows.

## 3. Account Lockout Policy

Ainda dentro de:

```text
Account Policies
```

foi acessada a categoria:

```text
Account Lockout Policy
```

Foram observadas as seguintes configurações:

* Account lockout duration
* Account lockout threshold
* Reset account lockout counter after

Essas políticas estão relacionadas ao bloqueio de contas após determinadas tentativas de autenticação malsucedidas.

### Account lockout threshold

Define a quantidade de tentativas de logon inválidas que pode provocar o bloqueio da conta.

Esse mecanismo pode ajudar a reduzir ataques baseados em tentativas repetidas de autenticação.

### Account lockout duration

Define por quanto tempo uma conta permanece bloqueada após atingir o limite configurado.

### Reset account lockout counter after

Define o período necessário para que o contador de tentativas inválidas seja reiniciado.

## 4. Local Policies

Na sequência, foi acessada:

```text
Local Policies
```

Essa seção reúne diferentes controles relacionados à segurança do sistema local.

Entre as categorias disponíveis está:

```text
Audit Policy
```

## 5. Audit Policy

A política de auditoria permite determinar quais tipos de eventos de segurança devem ser registrados pelo Windows.

Durante a atividade foram observadas as seguintes categorias:

* Audit account logon events
* Audit account management
* Audit directory service access
* Audit logon events
* Audit object access
* Audit policy change
* Audit privilege use
* Audit process tracking
* Audit system events

Essas configurações são importantes para o monitoramento do sistema porque podem gerar registros que posteriormente serão analisados para identificar atividades administrativas, autenticações, alterações de políticas, utilização de privilégios e outros eventos.

### Exemplos

**Audit account logon events**

Relaciona-se ao registro de eventos associados ao processo de autenticação de contas.

**Audit account management**

Permite auditar determinadas operações de gerenciamento de contas.

**Audit logon events**

Relaciona-se aos eventos de logon no sistema.

**Audit object access**

Pode registrar acessos a determinados objetos, conforme a configuração de auditoria e as SACLs aplicáveis.

**Audit policy change**

Permite registrar alterações nas políticas de auditoria.

**Audit privilege use**

Relaciona-se ao uso de determinados privilégios do sistema.

**Audit process tracking**

Permite acompanhar determinados eventos relacionados à execução de processos.

**Audit system events**

Relaciona-se a eventos importantes gerados pelo próprio sistema.

## 6. User Rights Assignment

Também foi explorada a categoria:

```text
Local Policies → User Rights Assignment
```

Essa seção define quais usuários ou grupos possuem determinados direitos no sistema.

Os direitos atribuídos podem controlar, por exemplo:

* ações permitidas localmente;
* logon e acesso ao sistema;
* execução de determinadas operações administrativas;
* utilização de privilégios específicos.

O conceito é importante porque uma conta possuir acesso ao sistema não significa necessariamente que ela tenha todos os privilégios disponíveis.

A atribuição de direitos permite aplicar o princípio do **menor privilégio**, concedendo somente as permissões necessárias para determinada função.

## 7. Security Options

Por fim, foi acessada:

```text
Local Policies → Security Options
```

Entre as configurações observadas estavam:

```text
Accounts: Administrator account status
Accounts: Guest account status
Devices: Allow undock without having to log on
Domain member: Digitally encrypt or sign secure channel data
Domain member: Disable machine account password changes
Interactive logon: Do not display last user name
Interactive logon: Do not require CTRL+ALT+DEL
```

Essas opções permitem configurar comportamentos específicos relacionados às contas, dispositivos, membros de domínio e processos de autenticação interativa.

### Accounts: Administrator account status

Controla o status da conta administrativa interna do Windows.

### Accounts: Guest account status

Controla o status da conta de convidado.

### Devices: Allow undock without having to log on

Define uma configuração relacionada à remoção de dispositivos de encaixe sem a necessidade de autenticação.

### Domain member: Digitally encrypt or sign secure channel data

Relaciona-se à proteção das comunicações do canal seguro entre um computador membro e o domínio.

### Domain member: Disable machine account password changes

Controla o comportamento relacionado à alteração das senhas das contas de computador em um domínio.

### Interactive logon: Do not display last user name

Controla se o nome do último usuário que realizou logon deve ser apresentado na tela de autenticação.

### Interactive logon: Do not require CTRL+ALT+DEL

Define se a combinação `CTRL+ALT+DEL` será exigida antes do processo de autenticação interativa.

## 8. Relação com a segurança do sistema

A Política de Segurança Local concentra diversos controles que podem ser utilizados para fortalecer a configuração de um servidor Windows.

A atividade permitiu observar diferentes camadas:

| Categoria              | Finalidade                                       |
| ---------------------- | ------------------------------------------------ |
| Password Policy        | Requisitos e ciclo de vida das senhas            |
| Account Lockout Policy | Controle de tentativas inválidas de autenticação |
| Audit Policy           | Registro de eventos de segurança                 |
| User Rights Assignment | Definição de direitos dos usuários e grupos      |
| Security Options       | Configurações adicionais de segurança do sistema |

Essas configurações trabalham em conjunto. Por exemplo, uma política de senha pode aumentar os requisitos para criação de credenciais, enquanto uma política de bloqueio pode limitar tentativas repetidas de autenticação e a auditoria pode fornecer registros para posterior investigação.

## 9. Resultado

A atividade permitiu explorar a ferramenta **Local Security Policy** do Windows Server 2022 e identificar as principais categorias de políticas de segurança.

Foram observadas:

1. Políticas de senha;
2. Políticas de bloqueio de contas;
3. Políticas de auditoria;
4. Direitos atribuídos a usuários;
5. Opções adicionais de segurança;
6. Configurações relacionadas à autenticação;
7. Controles relacionados a contas locais e membros de domínio.

O exercício reforçou a importância da configuração adequada das políticas de segurança e da geração de eventos de auditoria para o monitoramento e investigação de atividades no Windows Server.

## Evidência

A evidência da atividade está no PDF geral das Aulas 7 e 8:

[Ver evidências — Aulas 7 e 8](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-07-08/evidencias.pdf)

**Print registrado:** etapa 7 da atividade, conforme solicitado pelo roteiro.
