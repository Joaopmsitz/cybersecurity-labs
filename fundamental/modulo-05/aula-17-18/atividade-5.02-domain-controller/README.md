# Atividade 5.2 — Criando o Domain Controller do Active Directory

## Objetivo

Promover o servidor **Windows Server 2022** a **Domain Controller (DC)** do Active Directory, criando uma nova floresta e configurando o DNS do domínio.

Nesta atividade também é criada uma **Reverse Lookup Zone** para a rede utilizada pelo laboratório.

---

## Ambiente

* Windows Server 2022
* Active Directory Domain Services
* Domain Controller
* DNS Server
* DNS Manager
* Domínio: `aluno.hacker.com`
* NetBIOS: `ALUNO`
* Rede do laboratório: `192.168.98.0/24`

---

## 1. Iniciando a promoção do servidor

Após a instalação do AD DS na atividade anterior, o **Server Manager** apresentou uma notificação indicando que era necessário configurar o serviço.

No canto superior direito, foi selecionado o ícone de notificação e, em seguida:

```text id="tqyk5q"
Promote this server to a domain controller
```

Foi iniciado o assistente de configuração do Active Directory Domain Services.

---

## 2. Criando uma nova floresta

No **Deployment Configuration**, foi selecionada a opção:

```text id="h0c9jf"
Add a new forest
```

No campo **Root domain name**, foi informado:

```text id="v48kpo"
aluno.hacker.com
```

Em seguida, o assistente foi avançado.

---

## 3. Configurando a senha do Directory Services Restore Mode

Na etapa **Domain Controller Options**, foi definida a senha do:

```text id="y4ib2g"
Directory Services Restore Mode (DSRM)
```

A mesma senha foi informada nos campos **Password** e **Confirm Password**.

> A senha utilizada no laboratório não é registrada neste README.

Após a configuração, o assistente foi avançado para as próximas etapas.

---

## 4. Verificando o nome NetBIOS

Na etapa **Additional Options**, foi verificado o nome NetBIOS do domínio.

O valor apresentado foi:

```text id="1w4j4e"
ALUNO
```

O assistente foi avançado pelas etapas seguintes até chegar à verificação dos pré-requisitos.

---

## 5. Verificando os pré-requisitos

Na tela **Prerequisites Check**, foi verificado o resultado da validação.

O Windows Server apresentou o indicador verde e a mensagem:

```text id="9b5r6c"
All prerequisite checks passed successfully....
```

Após a validação, foi selecionado:

```text id="qj9n9g"
Install
```

A instalação iniciou a configuração do domínio e a promoção do servidor a Domain Controller.

Após a conclusão, o servidor foi reiniciado automaticamente.

---

## 6. Acessando novamente o servidor

Após aguardar a inicialização do Windows Server, foi estabelecida novamente a conexão RDP com:

```text id="jpm8vr"
192.168.98.20
```

O acesso foi realizado com a conta administrativa do laboratório.

Após a autenticação, o **Server Manager** foi aberto novamente.

Foi verificado que os serviços relacionados ao domínio estavam disponíveis, incluindo:

```text id="8m2x89"
AD DS
DNS
File and Storage Services
```

---

## 7. Abrindo o DNS Manager

No **Server Manager**, foi acessado:

```text id="7j1y4x"
Tools
    ↓
DNS
```

No **DNS Manager**, foi expandido:

```text id="h3a3z7"
DC01
└── Forward Lookup Zones
    └── aluno.hacker.com
```

A zona de pesquisa direta do domínio estava disponível.

---

## 8. Criando a Reverse Lookup Zone

No **DNS Manager**, foi selecionado:

```text id="x4k8x1"
Reverse Lookup Zones
```

Com o botão direito, foi selecionado:

```text id="x9n7jj"
New Zone...
```

O assistente foi avançado mantendo as opções indicadas pelo laboratório.

No campo **Network ID**, foi informado:

```text id="h7wq5f"
192.168.98
```

O assistente foi concluído através de:

```text id="kq4r6x"
Finish
```

A zona reversa passou então a aparecer dentro de:

```text id="w0m2gi"
Reverse Lookup Zones
```

---

## 9. Verificando a Reverse Lookup Zone

A zona recém-criada foi aberta:

```text id="2wqz4j"
Reverse Lookup Zones
└── 98.168.192.in-addr.arpa
```

Esta configuração representa a rede:

```text id="5h0o8m"
192.168.98.0/24
```

A criação da zona reversa permite realizar consultas DNS que partem de um endereço IP para obter informações de nome associadas.

A evidência solicitada pelo laboratório corresponde a esta etapa.

---

## 10. Verificando o Start of Authority

Dentro da zona:

```text id="l0y0qv"
98.168.192.in-addr.arpa
```

foi acessado:

```text id="6m3q0j"
Start of Authority (SOA)
```

Na janela aberta, foi acessada a aba:

```text id="3w8j7r"
Name Servers
```

Foi selecionado o servidor e utilizada a opção:

```text id="1a4q8x"
Edit...
```

Em seguida, foi selecionado:

```text id="c5x7dp"
Resolve
```

O servidor apresentou a resolução com o indicador verde de sucesso.

---

## 11. Atualizando o registro PTR

Ainda no **DNS Manager**, foi acessada a zona direta:

```text id="v5q9gk"
DC01
└── Forward Lookup Zones
    └── aluno.hacker.com
```

Foi selecionado o registro do servidor `dc01`.

Na janela de propriedades, foi habilitada a opção:

```text id="x8o6g3"
Update associated pointer (PTR) record
```

A alteração foi confirmada.

---

## 12. Verificando o registro na zona reversa

Por fim, foi retornada a:

```text id="q1v6n8"
Reverse Lookup Zones
└── 98.168.192.in-addr.arpa
```

Foi utilizado o botão **Refresh** para atualizar a visualização.

Após a atualização, apareceu um novo elemento relacionado ao endereço IP do servidor.

---

## Conceitos

### Domain Controller

O **Domain Controller** é o servidor responsável por fornecer os serviços centrais de autenticação e gerenciamento de um domínio do Active Directory.

Nesta atividade, o `DC01` foi promovido a controlador do domínio:

```text id="t4w2o9"
aluno.hacker.com
```

### Floresta

Uma **forest** é a estrutura de nível mais alto do Active Directory que agrupa um ou mais domínios e compartilha elementos como esquema e configuração.

Nesta atividade foi criada uma nova floresta através da opção:

```text id="s0h2r5"
Add a new forest
```

### DNS Forward Lookup Zone

A zona de pesquisa direta é utilizada para resolver nomes para endereços IP.

No laboratório:

```text id="6c4t9a"
aluno.hacker.com
```

foi configurada como zona direta.

### Reverse Lookup Zone

A zona de pesquisa reversa realiza o processo inverso, permitindo consultar informações DNS a partir de um endereço IP.

Para a rede do laboratório, foi criada:

```text id="n8f5b2"
98.168.192.in-addr.arpa
```

correspondente à rede:

```text id="h4z2x6"
192.168.98.0/24
```

### Registro PTR

O registro **PTR (Pointer)** é utilizado em consultas DNS reversas para associar um endereço IP a um nome.

A opção:

```text id="3s6n4w"
Update associated pointer (PTR) record
```

permite atualizar o registro PTR relacionado ao servidor.

### Registro SOA

O **Start of Authority (SOA)** contém informações administrativas sobre uma zona DNS, como o servidor autoritativo e parâmetros relacionados à manutenção da zona.

---

## Resultado

O servidor `DC01` foi promovido a **Domain Controller** e uma nova floresta foi criada utilizando o domínio:

```text id="c7m3w1"
aluno.hacker.com
```

Também foi configurada a zona DNS reversa:

```text id="9z4x6k"
98.168.192.in-addr.arpa
```

correspondente à rede `192.168.98.0/24`.

Por fim, foi verificada a resolução do servidor e habilitada a atualização do registro PTR associado ao endereço IP do `DC01`.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 1 e 2**](../evidencias.pdf)

**Evidência registrada:** passo 9 — criação e visualização da **Reverse Lookup Zone** `98.168.192.in-addr.arpa`.
