# Atividade 5.3 — Inserindo um usuário no Domínio do Active Directory

## Objetivo

Criar um usuário no domínio do Active Directory, configurar sua associação ao grupo **Remote Desktop Users** e criar uma **Group Policy Object (GPO)** para permitir o acesso de usuários do domínio através do Remote Desktop Services.

---

## Ambiente

* Windows Server 2022
* Active Directory
* Active Directory Users and Computers
* Group Policy Management
* Group Policy Management Editor
* Domínio: `aluno.hacker.com`
* Usuário criado: `nome1`
* Unidade Organizacional: `Rede1`
* GPO: `Alunos`

---

## 1. Criando o usuário no Active Directory

No **Server Manager**, foi acessado:

```text id="9g0c5x"
Tools
    ↓
Active Directory Users and Computers
```

No painel esquerdo, foi expandido:

```text id="5p4k1d"
aluno.hacker.com
└── Users
```

Na área de usuários, foi selecionado:

```text id="n7m4z2"
New
    ↓
User
```

Foram preenchidos os dados do novo usuário:

```text id="1q6x8v"
First name: Nome1
Last name: Sobrenome1
User logon name: nome1
```

Foi definida uma senha para o usuário.

> A senha utilizada no laboratório não é registrada neste README.

Também foi desmarcada a opção:

```text id="0h4r6k"
User must change password at next logon
```

e habilitada:

```text id="3m8v2p"
Password never expires
```

Após concluir o assistente, o usuário **Nome1 Sobrenome1** passou a aparecer na lista de usuários do domínio.

---

## 2. Adicionando o usuário ao Remote Desktop Users

Com o usuário criado, foram abertas suas propriedades:

```text id="j6s2w9"
Nome1 Sobrenome1
    ↓
Properties
```

Na aba:

```text id="w1k5q8"
Member of
```

foi selecionado:

```text id="e9r3c7"
Add...
```

Na janela de seleção de grupos, foi pesquisado:

```text id="x4v7m2"
remote
```

Após utilizar **Check Names**, foi selecionado:

```text id="p5n8d1"
Remote Desktop Users
```

A alteração foi confirmada com **OK**, seguida de **Apply** e **OK**.

---

## 3. Abrindo o Group Policy Management

No **Server Manager**, foi acessado:

```text id="7b3k9m"
Tools
    ↓
Group Policy Management
```

No painel esquerdo, foi expandida a estrutura:

```text id="a2f6q4"
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
```

---

## 4. Criando a Organizational Unit

Com o botão direito sobre:

```text id="v8j3x5"
aluno.hacker.com
```

foi selecionado:

```text id="r6m1k9"
New Organizational Unit
```

A nova unidade organizacional recebeu o nome:

```text id="q3z7w2"
Rede1
```

Após confirmar, a OU `Rede1` passou a aparecer dentro do domínio.

---

## 5. Criando a GPO

Com o botão direito sobre a OU:

```text id="n4c8y6"
Rede1
```

foi selecionada:

```text id="t2p5s9"
Create a GPO in this domain, and Link it here...
```

A política recebeu o nome:

```text id="u7h3k1"
Alunos
```

Após a criação, a GPO passou a aparecer vinculada à OU `Rede1`.

---

## 6. Editando a GPO

Com o botão direito sobre a GPO:

```text id="d5m9q2"
Alunos
```

foi selecionado:

```text id="f8x4v6"
Edit...
```

No **Group Policy Management Editor**, foi seguida a estrutura:

```text id="s1k7w3"
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── User Rights Assignment
```

Na lista de políticas, foi aberta:

```text id="z6p2r8"
Allow log on through Remote Desktop Services
```

---

## 7. Adicionando Domain Users

Na janela da política, foi habilitada:

```text id="c4v8n1"
Define these policy settings
```

Em seguida:

```text id="h7m3x9"
Add User or Group...
    ↓
Browse...
    ↓
Advanced
    ↓
Find Now
```

Na lista apresentada, foi selecionado:

```text id="k2q6w5"
Domain Users
```

---

## 8. Adicionando Authenticated Users

O processo de seleção de usuários e grupos foi repetido:

```text id="b9r4t7"
Advanced
    ↓
Find Now
```

Foi selecionado:

```text id="m5x8c3"
Authenticated Users
```

As alterações foram confirmadas com:

```text id="v2n6p9"
OK
OK
Apply
OK
```

Com isso, a configuração da política passou a permitir os grupos selecionados na política de logon através do Remote Desktop Services.

---

## 9. Atualizando as políticas

Na barra de tarefas do Windows, foi aberto o **Command Prompt** através da pesquisa por:

```text id="q8s1f4"
cmd
```

Foi executado:

```cmd id="c0m7y5"
gpupdate /force
```

Saída apresentada no laboratório:

```text id="a7x3k9"
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

A evidência solicitada pelo laboratório corresponde a esta etapa.

---

## Conceitos

### Active Directory Users and Computers

O **Active Directory Users and Computers (ADUC)** é uma ferramenta administrativa utilizada para gerenciar objetos do domínio, como:

* usuários;
* grupos;
* computadores;
* unidades organizacionais.

Nesta atividade, foi utilizado para criar o usuário `nome1`.

### Grupo Remote Desktop Users

O grupo **Remote Desktop Users** permite organizar usuários que possuem autorização para utilizar determinados recursos de acesso remoto, conforme as políticas configuradas no sistema.

O usuário criado foi adicionado a esse grupo durante a atividade.

### Group Policy Object (GPO)

Uma **GPO** é um conjunto de configurações que pode ser aplicado a usuários e computadores de um domínio.

Neste laboratório, foi criada a GPO:

```text id="e3j8q1"
Alunos
```

e vinculada à OU:

```text id="n6w2r5"
Rede1
```

### User Rights Assignment

A seção **User Rights Assignment** permite definir direitos atribuídos a usuários e grupos no Windows.

A política utilizada foi:

```text id="p1c7v4"
Allow log on through Remote Desktop Services
```

Ela controla quais usuários ou grupos podem receber o direito de realizar logon através dos serviços de Remote Desktop.

### gpupdate /force

O comando:

```cmd id="u9k5d2"
gpupdate /force
```

solicita a atualização imediata das políticas de grupo no computador.

A opção `/force` força a reaplicação das configurações de política, mesmo quando elas não aparentam ter sido alteradas desde a última atualização.

---

## Resultado

Foi criado o usuário:

```text id="r4m8x6"
Nome1 Sobrenome1
```

no domínio:

```text id="y2q7n5"
aluno.hacker.com
```

O usuário foi associado ao grupo **Remote Desktop Users**.

Também foi criada a OU:

```text id="c8w3p1"
Rede1
```

e a GPO:

```text id="f6m2z9"
Alunos
```

A política **Allow log on through Remote Desktop Services** foi configurada para incluir `Domain Users` e `Authenticated Users`.

Por fim, o comando `gpupdate /force` confirmou a aplicação das políticas:

```text id="s5v1k8"
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

---

## Evidências

[**Evidências — Módulo 5 / Aulas 1 e 2**](../evidencias.pdf)

**Evidência registrada:** passo 11 — execução do `gpupdate /force` e confirmação da atualização das políticas.
