# Atividade 9.2 — Emitindo Certificados Digitais usando uma Autoridade Certificadora

## Objetivo

Utilizar a Autoridade Certificadora criada na atividade anterior para configurar um **template de certificado**, disponibilizá-lo na CA e configurar o **autoenrollment** por meio de uma política de grupo.

Ao final, foi utilizado o comando `gpupdate /force` para aplicar as políticas configuradas e verificar a emissão de um certificado para o ambiente.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Serviço:** Active Directory Certificate Services (AD CS)
* **Autoridade Certificadora:** `aluno-DC01-CA`
* **Domínio:** `aluno.hacker.com`
* **Template criado:** `ALUNO COMPUTADOR`
* **GPO:** `COMPUTADOR: Politica de Inscricao de Certificado`
* **Mecanismo:** Certificate Auto-Enrollment

---

## 1. Acesso aos templates da Autoridade Certificadora

Na janela **Certification Authority (Local)**, foi expandida a autoridade:

```text
aluno-DC01-CA
```

Em seguida, foi acessada a opção:

```text
Certificate Templates → Manage
```

Foi aberta a janela **Certificate Template Console**.

---

## 2. Duplicação do template

Na lista de templates disponíveis, foi localizado:

```text
Workstation Authentication
```

O template foi selecionado com o botão direito e utilizada a opção:

```text
Duplicate Template
```

A duplicação permitiu criar um novo template baseado nas configurações do modelo existente.

---

## 3. Criação do template ALUNO COMPUTADOR

Na janela **Properties of New Template**, foi acessada a aba:

```text
General
```

O campo **Template display name** foi alterado para:

```text
ALUNO COMPUTADOR
```

Esse será o nome utilizado para identificar o novo template dentro da infraestrutura de certificados.

---

## 4. Configuração do Subject Name

Na aba:

```text
Subject Name
```

foi habilitada a opção:

```text
User principal name (UPN)
```

Essa configuração permite que o UPN seja utilizado na identificação associada ao certificado emitido.

---

## 5. Configuração das permissões

Na aba:

```text
Security
```

foi selecionado:

```text
Domain Computers (ALUNO\Domain Computers)
```

Para esse grupo, foram habilitadas as permissões **Allow** para:

```text
Read
Autoenroll
```

As alterações foram aplicadas utilizando **Apply** e **OK**.

Após a configuração, o novo template passou a aparecer como:

```text
ALUNO COMPUTADOR
```

---

## 6. Disponibilização do template na CA

De volta à janela **Certification Authority (Local)**, foi acessada a opção:

```text
Certificate Templates → New → Certificate Template to Issue
```

Na janela **Enable Certificate Templates**, foi selecionado:

```text
ALUNO COMPUTADOR
```

e confirmada a operação com **OK**.

O template passou então a estar disponível para emissão pela Autoridade Certificadora.

---

## 7. Verificação do template

Ao selecionar a pasta:

```text
Certificate Templates
```

foi possível verificar o template:

```text
ALUNO COMPUTADOR
```

na coluna da direita.

Isso indica que a CA está configurada para utilizar esse template na emissão de certificados.

---

## 8. Acesso ao Group Policy Management

No **Server Manager**, foi acessado:

```text
Tools → Group Policy Management
```

Na árvore do domínio, foi expandido:

```text
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
        └── Group Policy Objects
```

Foi criada uma nova política de grupo.

---

## 9. Criação da GPO

A nova GPO recebeu o nome:

```text
COMPUTADOR: Politica de Inscricao de Certificado
```

A política foi criada dentro de:

```text
Group Policy Objects
```

---

## 10. Edição da política

A GPO recém-criada foi aberta com **Edit**.

No **Group Policy Management Editor**, foi seguido o caminho:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Public Key Policies
```

Foi selecionado:

```text
Certificate Services Client – Auto-Enrollment
```

---

## 11. Configuração do Auto-Enrollment

Na configuração de **Certificate Services Client – Auto-Enrollment**, o campo:

```text
Configuration Model
```

foi alterado de:

```text
Not configured
```

para:

```text
Enabled
```

Também foram habilitadas as opções relacionadas à renovação e atualização dos certificados:

```text
Renew expired certificates...
Update certificates...
```

As alterações foram confirmadas com **Apply** e **OK**.

---

## 12. Configuração do Automatic Certificate Request

Na coluna da direita do **Group Policy Management Editor**, foi acessada:

```text
Automatic Certificate Request Settings
```

Com o botão direito, foi selecionado:

```text
New → Automatic Certificate Request...
```

O assistente foi avançado utilizando **Next** até a conclusão com **Finish**.

---

## 13. Atualização das políticas

Para aplicar imediatamente as configurações realizadas, foi aberto o **Command Prompt**.

Foi executado:

```cmd
gpupdate /force
```

O comando força a atualização das políticas de grupo aplicáveis ao computador e ao usuário.

---

## 14. Resultado da atualização

Após a execução do comando, o Windows apresentou:

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

Esse resultado indica que tanto a política do computador quanto a política do usuário foram atualizadas com sucesso.

---

## 15. Verificação da emissão

Após a atualização das políticas, foi retornada a janela:

```text
certsrv - [Certification Authority (Local)]
```

Na pasta:

```text
Issued Certificates
```

foi verificada a emissão de um certificado.

Isso demonstra a aplicação da política de inscrição configurada e a utilização da Autoridade Certificadora para emissão do certificado.

---

## 16. Encerramento da sessão do servidor

Após a verificação da emissão, a sessão RDP com o Windows Server 2022 utilizado como servidor foi encerrada.

O ambiente ficou preparado para a próxima atividade, na qual o certificado emitido será analisado no Windows Server 2022 utilizado como cliente.

---

## Evidência — Passo 17

A evidência solicitada para esta atividade corresponde ao **passo 17**, contendo a execução do `gpupdate /force` e o resultado positivo da atualização das políticas.

**Frase obrigatória antes do print:**

> **Print da atividade 9.2:** execução do comando `gpupdate /force`, demonstrando que as políticas do computador e do usuário foram atualizadas com sucesso.

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

[**Evidências — Módulo 9 / Aulas 33 e 34**](../evidencias.pdf)

---

## Conceitos aplicados

### Certificate Template

Um **Certificate Template** define as características e regras utilizadas pela Autoridade Certificadora para emitir determinados tipos de certificados.

Neste laboratório, o template:

```text
ALUNO COMPUTADOR
```

foi criado a partir do template `Workstation Authentication`.

### Auto-Enrollment

O **autoenrollment** permite que certificados sejam automaticamente solicitados e gerenciados pelos computadores ou usuários que atendem às condições definidas nas políticas do domínio.

### Group Policy

As **Group Policies (GPOs)** permitem distribuir configurações de forma centralizada para computadores e usuários pertencentes ao domínio.

Neste exercício, uma GPO foi utilizada para configurar o comportamento de inscrição automática de certificados.

### Certificate Authority

A CA `aluno-DC01-CA`, configurada na atividade anterior, foi utilizada para disponibilizar o template e emitir certificados para os computadores do domínio.

---

## Fluxo da atividade

```text
Template Workstation Authentication
              │
              ▼
       Duplicate Template
              │
              ▼
      ALUNO COMPUTADOR
              │
              ▼
      Publicação na CA
              │
              ▼
       Criação da GPO
              │
              ▼
       Auto-Enrollment
              │
              ▼
        gpupdate /force
              │
              ▼
      Emissão do certificado
```

---

## Resultado

Foi criado e disponibilizado na Autoridade Certificadora o template:

```text
ALUNO COMPUTADOR
```

Também foi configurada uma política de grupo para permitir o **autoenrollment** de certificados para `Domain Computers`.

A aplicação da política foi confirmada com:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

Posteriormente, a pasta **Issued Certificates** da CA foi utilizada para verificar a emissão do certificado.
