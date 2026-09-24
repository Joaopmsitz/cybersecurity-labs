# Atividade 5.5 — Configurando Política de Senhas no GPO do Windows Server 2022

## Objetivo

Criar e configurar uma **Group Policy Object (GPO)** para estabelecer uma política de senhas no domínio do Active Directory.

Nesta atividade foram configurados requisitos relacionados à validade, comprimento, complexidade e histórico das senhas.

---

## Ambiente

* Windows Server 2022
* Active Directory
* Group Policy Management
* Group Policy Management Editor
* Domínio: `aluno.hacker.com`
* GPO: `Politica de senhas`

---

## 1. Abrindo o Group Policy Management

O Windows Server 2022 servidor foi acessado através de RDP.

```text id="n4q8w2"
IP: 192.168.98.20
Usuário: Administrator
```

As credenciais utilizadas pertencem ao ambiente do laboratório e não são registradas neste documento.

No **Server Manager**, foi acessado:

```text id="c7m3x9"
Tools
    ↓
Group Policy Management
```

---

## 2. Localizando o domínio

No painel esquerdo do **Group Policy Management**, foi expandida a estrutura:

```text id="v2p6k8"
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
```

Dentro do domínio foi localizada a pasta:

```text id="j5r9w3"
Group Policy Objects
```

---

## 3. Criando a GPO

Com o botão direito sobre:

```text id="a8q4m1"
Group Policy Objects
```

foi selecionada a opção:

```text id="x6n2c7"
New
```

A nova política recebeu o nome:

```text id="f3v8p5"
Politica de senhas
```

Após confirmar, a GPO passou a aparecer na lista de objetos de política do domínio.

---

## 4. Abrindo o editor da GPO

Com o botão direito sobre:

```text id="y7k1q4"
Politica de senhas
```

foi selecionado:

```text id="m9c5x2"
Edit
```

Foi aberta a janela **Group Policy Management Editor**.

---

## 5. Localizando as configurações de senha

No painel esquerdo, foi seguida a estrutura:

```text id="p4w8n6"
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Password Policy
```

Nessa seção estão disponíveis configurações relacionadas ao gerenciamento das senhas do domínio.

---

## 6. Configurando a idade máxima da senha

Foi aberta a política:

```text id="q2m7v9"
Maximum password age
```

A opção:

```text id="r5x1c8"
Define this policy setting
```

foi habilitada.

Foi definido:

```text id="k6p3w4"
120 dias
```

A configuração foi aplicada através de:

```text id="s8n2q5"
Apply
    ↓
OK
```

Essa configuração determina o período máximo antes que uma senha precise ser alterada.

---

## 7. Configurando o comprimento mínimo

Foi aberta:

```text id="u4c9m7"
Minimum password length
```

A configuração foi habilitada e definida como:

```text id="d1x6p8"
9 caracteres
```

Após a definição, foi selecionado:

```text id="g5r2v9"
Apply
    ↓
OK
```

A configuração estabelece o número mínimo de caracteres exigidos para as senhas.

---

## 8. Ativando a complexidade da senha

Foi aberta a configuração:

```text id="w3k8q1"
Password must meet complexity requirements
```

A opção de definição da política foi habilitada e o valor:

```text id="b7m4x6"
Enabled
```

foi selecionado.

A alteração foi aplicada e confirmada.

Com essa configuração, o Windows passa a exigir que as senhas atendam aos requisitos de complexidade definidos pelo sistema.

---

## 9. Configurando o histórico de senhas

Foi aberta:

```text id="n2p5c9"
Enforce password history
```

A política foi habilitada e configurada com:

```text id="f8v3m1"
3
```

Isso faz com que o Windows mantenha o histórico das últimas três senhas para impedir a reutilização imediata dessas credenciais.

A alteração foi aplicada e confirmada.

---

## 10. Vinculando a GPO ao domínio

De volta à janela **Group Policy Management**, foi selecionado o domínio:

```text id="q6x9w2"
aluno.hacker.com
```

Com o botão direito, foi escolhida:

```text id="h4m7p1"
Link an Existing GPO
```

Na lista de GPOs disponíveis, foi selecionada:

```text id="z8c3r5"
Politica de senhas
```

e confirmado com:

```text id="t1v6k9"
OK
```

A GPO passou a estar vinculada ao domínio.

---

## 11. Verificando a aplicação da GPO

Após o vínculo da política, foi aberto o **Command Prompt** através da pesquisa por:

```text id="e5q2m8"
cmd
```

Foi executado:

```cmd id="y9k4c6"
gpupdate /force
```

O comando foi utilizado para forçar a atualização das políticas de grupo.

---

## 12. Resultado da atualização das políticas

A saída apresentada no laboratório foi:

```text id="r7x2p5"
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

A mensagem confirma que as políticas de computador e de usuário foram atualizadas com sucesso.

A evidência solicitada pelo laboratório corresponde a esta etapa.

---

## Configurações aplicadas

A GPO **Politica de senhas** foi configurada com os seguintes parâmetros:

| Configuração             |        Valor |
| ------------------------ | -----------: |
| Maximum password age     |     120 dias |
| Minimum password length  | 9 caracteres |
| Password complexity      |   Habilitada |
| Enforce password history |     3 senhas |

A GPO foi vinculada ao domínio:

```text id="c4m8q1"
aluno.hacker.com
```

---

## Conceitos

### Group Policy Object (GPO)

Uma **GPO** é um conjunto de configurações administrativas que pode ser aplicado a usuários e computadores de um ambiente Windows.

Em um domínio Active Directory, as GPOs permitem centralizar diversas configurações de segurança e administração.

### Password Policy

A **Password Policy** reúne configurações que determinam requisitos para as senhas utilizadas no domínio.

Nesta atividade foram configurados:

* tempo máximo de validade;
* tamanho mínimo;
* complexidade;
* histórico de senhas.

### Password History

O histórico de senhas impede que o usuário reutilize imediatamente credenciais anteriores.

No laboratório, foram configuradas as últimas:

```text id="m6w3k8"
3 senhas
```

### Password Complexity

A configuração de complexidade determina requisitos adicionais para as senhas, aumentando a variedade de caracteres necessária de acordo com as regras do Windows.

### gpupdate /force

O comando:

```cmd id="s3q7n2"
gpupdate /force
```

força uma atualização das políticas de grupo no computador.

A saída:

```text id="v8p4x6"
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

indica que a atualização das políticas foi concluída com sucesso.

---

## Resultado

Foi criada a GPO:

```text id="j2c6m9"
Politica de senhas
```

com requisitos de:

* validade máxima de 120 dias;
* comprimento mínimo de 9 caracteres;
* complexidade habilitada;
* histórico das últimas 3 senhas.

A GPO foi vinculada ao domínio `aluno.hacker.com` e as políticas foram atualizadas com sucesso utilizando `gpupdate /force`.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 1 e 2**](../evidencias.pdf)

**Evidência registrada:** passo 12 — execução do `gpupdate /force` e confirmação da atualização das políticas de computador e usuário.
