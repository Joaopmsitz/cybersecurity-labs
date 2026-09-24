# Atividade 5.7 — Criando uma Organizational Unit (OU) no Windows Server 2022

## Objetivo

Criar uma **Organizational Unit (OU)** no Active Directory e adicionar um novo usuário dentro dessa estrutura.

Nesta atividade, foi criada a OU `TI` no domínio `aluno.hacker.com` e, dentro dela, um usuário chamado `usuarioti`.

O exercício demonstra a utilização de **Organizational Units (OUs)** e do **Common Name (CN)** na organização de objetos do Active Directory.

---

## Ambiente

* Windows Server 2022 — servidor / Domain Controller
* Active Directory Users and Computers
* Domínio: `aluno.hacker.com`
* OU criada: `TI`
* Usuário criado: `usuarioti`
* Nome do usuário: `Usuario TI`

---

## 1. Acessando o Windows Server 2022

Foi estabelecida uma conexão RDP com o Windows Server 2022 servidor:

```text id="8k2m4p"
192.168.98.20
```

O acesso foi realizado utilizando uma conta administrativa do domínio.

As credenciais utilizadas no laboratório não são registradas neste README.

---

## 2. Abrindo o Active Directory Users and Computers

Na barra de tarefas, foi utilizado o campo:

```text id="m6q9v2"
Type here to search
```

e pesquisado:

```text id="r3w7c1"
Active Directory Users and Computers
```

O aplicativo foi aberto a partir dos resultados da pesquisa.

---

## 3. Localizando o domínio

No painel esquerdo do **Active Directory Users and Computers**, foi localizado o domínio:

```text id="x5n8j4"
aluno.hacker.com
```

O domínio foi selecionado para visualizar os objetos existentes no Active Directory.

---

## 4. Criando a Organizational Unit

Com o botão direito sobre:

```text id="p7k2m9"
aluno.hacker.com
```

foi selecionado:

```text id="v4c8q1"
New
    ↓
Organizational Unit
```

Na janela apresentada, foi informado o nome:

```text id="t6x3w8"
TI
```

e confirmado com:

```text id="n9m5r2"
OK
```

A nova OU passou a aparecer na estrutura do domínio.

---

## 5. Verificando a OU criada

No painel esquerdo do **Active Directory Users and Computers**, a estrutura passou a apresentar:

```text id="h2q7c5"
aluno.hacker.com
└── TI
```

A OU `TI` será utilizada para organizar o usuário criado nesta atividade.

---

## 6. Criando um usuário dentro da OU

Foi selecionada a OU:

```text id="j8w4p1"
TI
```

Com o botão direito, foi acessado:

```text id="f3m9x6"
New
    ↓
User
```

Foi aberta a janela de criação de um novo usuário.

---

## 7. Preenchendo os dados do usuário

Nos campos de identificação foram inseridos:

```text id="c5v2n8"
First name:
Usuario
```

```text id="q1r7m4"
Last name:
TI
```

No campo:

```text id="z6x3p9"
User logon name
```

foi informado:

```text id="w8k4c2"
usuarioti
```

O valor `usuarioti` corresponde ao nome de logon utilizado pelo novo usuário e representa o **Common Name (CN)** considerado no exercício.

**Esta é a etapa solicitada como evidência da atividade.**

---

## 8. Configurando a senha

Foi selecionado:

```text id="g5n2v7"
Next
```

Na etapa seguinte, foi definida a senha do usuário conforme as instruções do laboratório.

A opção:

```text id="a9c4x1"
User must change password at next logon
```

foi desmarcada.

Também foi habilitada:

```text id="s7m3q8"
Password never expires
```

A senha utilizada no laboratório não é registrada neste README.

---

## 9. Finalizando a criação do usuário

Foi selecionado:

```text id="d2k8w5"
Next
    ↓
Finish
```

O usuário foi criado com sucesso dentro da OU `TI`.

A estrutura resultante ficou semelhante a:

```text id="v6p1x9"
aluno.hacker.com
└── TI
    └── Usuario TI
```

O usuário pode posteriormente ser administrado através do próprio **Active Directory Users and Computers**, permitindo alterações de propriedades, grupos, permissões e outras configurações relacionadas à conta.

---

## Conceitos

### Organizational Unit (OU)

Uma **Organizational Unit** é um objeto do Active Directory utilizado para organizar usuários, computadores e outros objetos dentro de uma estrutura lógica.

As OUs também podem ser utilizadas como escopo para aplicação e organização de **Group Policy Objects (GPOs)**.

Neste laboratório foi criada:

```text id="m8q4c7"
OU: TI
```

dentro do domínio:

```text id="x2v9p5"
aluno.hacker.com
```

### Common Name (CN)

O **Common Name (CN)** identifica um objeto dentro da estrutura do diretório.

No exercício, o usuário foi criado com:

```text id="r4k1w8"
usuarioti
```

como nome de logon.

### Active Directory Users and Computers

O **Active Directory Users and Computers (ADUC)** é uma ferramenta administrativa utilizada para gerenciar objetos do Active Directory, incluindo:

* usuários;
* grupos;
* computadores;
* Organizational Units;
* propriedades das contas;
* associação de objetos a grupos.

---

## Estrutura criada

Ao final da atividade, a organização do domínio ficou:

```text id="c9m5x2"
aluno.hacker.com
└── TI
    └── Usuario TI
```

Essa estrutura permite separar objetos de acordo com departamentos ou funções, facilitando posteriormente a administração do ambiente.

---

## Resultado

Foi criada a **Organizational Unit `TI`** dentro do domínio `aluno.hacker.com`.

Em seguida, foi criado dentro dessa OU o usuário:

```text id="y7q3n6"
Usuario TI
```

com o nome de logon:

```text id="p5c8m1"
usuarioti
```

A atividade demonstrou a criação e organização de objetos utilizando o Active Directory Users and Computers.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 3 e 4**](../evidencias.pdf)

**Evidência registrada:** passo 9 — finalização da criação do usuário `usuarioti` dentro da OU `TI`.
