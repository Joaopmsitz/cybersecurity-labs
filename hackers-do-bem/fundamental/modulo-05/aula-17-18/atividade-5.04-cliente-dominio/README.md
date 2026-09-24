# Atividade 5.4 — Configurando um Cliente Windows Server 2022 no Domínio

## Objetivo

Configurar um segundo Windows Server 2022 como cliente do domínio **Active Directory**, utilizando o `DC01` como servidor DNS e controlador de domínio.

Ao final da atividade, o cliente será associado ao domínio `aluno.hacker.com` e será realizado um acesso remoto utilizando o usuário criado no Active Directory.

---

## Ambiente

* Windows Server 2022 — servidor / Domain Controller
* Windows Server 2022 — cliente
* Active Directory Domain Services
* DNS
* Remote Desktop
* Domínio: `aluno.hacker.com`
* Servidor: `192.168.98.20`
* Cliente: `192.168.98.30`
* Usuário de domínio: `nome1`

---

## 1. Verificando o endereço IP do servidor

Com o Windows Server 2022 servidor conectado, foi aberto o **Command Prompt** através da pesquisa por:

```text id="x2f7m1"
cmd
```

Foi executado:

```cmd id="q8v4n6"
ipconfig
```

Saída relevante apresentada no laboratório:

```text id="3k6p9a"
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : ec2.internal
   Link-local IPv6 Address . . . . . : fe80::858e:1f4d:6a2:81ef%7
   IPv4 Address. . . . . . . . . . . : 192.168.98.20
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.98.1
```

O endereço `192.168.98.20` corresponde ao servidor que fornecerá os serviços de domínio e DNS para o cliente.

---

## 2. Acessando o Windows Server 2022 cliente

A conexão RDP com o servidor foi minimizada e foi estabelecida uma nova conexão com o segundo Windows Server 2022:

```text id="v5n8c2"
IP: 192.168.98.30
```

O acesso inicial foi realizado com a conta administrativa do laboratório.

Os próximos procedimentos foram executados no Windows Server 2022 **cliente**.

---

## 3. Testando a comunicação com o Domain Controller

No cliente, foi aberto o **Command Prompt** e executado:

```cmd id="m3q7w1"
ping 192.168.98.20
```

Saída observada no material do laboratório:

```text id="p9x4k6"
C:\Users\Administrator>ping 192.168.98.20

Pinging 192.168.98.20 with 32 bytes of data:
Reply from 192.168.98.20: bytes=32 time=1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.98.20:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

O resultado demonstra que o cliente conseguiu alcançar o servidor pela rede, com:

```text id="r6c2m8"
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

---

## 4. Configurando o DNS do cliente

No cliente, foi aberto:

```text id="y7p3n5"
Control Panel
    ↓
Network and Internet
    ↓
Network and Sharing Center
```

Foi acessada a conexão Ethernet e aberta a configuração:

```text id="f2k8q4"
Internet Protocol Version 4 (TCP/IP)
```

Foi selecionada a opção:

```text id="c9v1x6"
Use the following DNS server addresses
```

O servidor DNS preferencial foi configurado para:

```text id="h4m7s2"
192.168.98.20
```

Esse endereço corresponde ao `DC01`, que fornece o serviço DNS utilizado pelo domínio.

As alterações foram confirmadas e as janelas foram fechadas.

---

## 5. Instalando o Remote Assistance

No **Server Manager**, foi acessado:

```text id="n8q5w3"
Manage
    ↓
Add Roles and Features
```

O assistente foi avançado até a tela **Features**.

Foi habilitado:

```text id="b6x2p9"
Remote Assistance
```

Em seguida, foi selecionado:

```text id="j3m7c5"
Next
    ↓
Install
```

Após a conclusão da instalação, foi selecionado:

```text id="z4r8v1"
Close
```

---

## 6. Associando o cliente ao domínio

No cliente, foram abertas as propriedades avançadas do sistema através de:

```text id="w5k2q7"
System
    ↓
Advanced system settings
```

Na janela **System Properties**, foi acessada a aba:

```text id="s9c3m6"
Computer Name
```

Foi selecionado:

```text id="p7x1n4"
Change
```

Na seção de associação ao domínio, foi selecionada:

```text id="e2v6k8"
Domain
```

e informado:

```text id="u4q9y3"
aluno.hacker.com
```

Foi solicitado o fornecimento das credenciais do usuário de domínio criado anteriormente.

> As credenciais utilizadas no laboratório não são registradas neste documento.

Após a autenticação, o Windows confirmou a entrada do computador no domínio.

Foram confirmadas as mensagens apresentadas e o sistema foi reiniciado.

---

## 7. Configurando o acesso remoto para o usuário do domínio

Após a reinicialização, foi acessada novamente a janela:

```text id="a8m3v6"
System Properties
    ↓
Remote
```

Foi habilitada a opção:

```text id="q5r7x2"
Allow connections only from...
```

Em seguida, foi selecionado:

```text id="k1c9w4"
Select Users...
```

e:

```text id="t6p2n8"
Add...
    ↓
Advanced...
    ↓
Find Now
```

Na lista apresentada, foi localizado:

```text id="d4y8m1"
Nome1 Sobrenome1
```

O usuário foi selecionado e confirmado.

Após a configuração, o usuário de domínio apareceu na lista de usuários autorizados para acesso remoto.

---

## 8. Encerrando a sessão administrativa

Após concluir as configurações, foi utilizado:

```text id="g7q3v5"
Shut down or sign out
    ↓
Sign out
```

A sessão administrativa foi encerrada.

---

## 9. Estabelecendo uma nova conexão RDP

Foi estabelecida uma nova conexão RDP com o cliente:

```text id="m2x6p9"
192.168.98.30
```

Foi utilizado o usuário de domínio:

```text id="v8c4r1"
nome1
```

As credenciais correspondentes pertencem ao ambiente do laboratório e não são publicadas neste README.

> O perfil RDP anterior não deveria ser reutilizado, pois ele continha as credenciais da conta administrativa utilizada anteriormente.

Na conexão, foi selecionado o domínio:

```text id="n5w7q2"
aluno.hacker.com
```

Após a autenticação, o usuário de domínio conseguiu acessar o Windows Server 2022 cliente.

A evidência solicitada pelo laboratório corresponde a esta etapa.

---

## Conceitos

### Cliente de domínio

Um computador associado a um domínio do Active Directory pode utilizar os serviços centralizados fornecidos pelo Domain Controller para autenticação e gerenciamento.

Neste laboratório, o Windows Server 2022 cliente foi associado ao:

```text id="r3k8m5"
aluno.hacker.com
```

### DNS e Active Directory

O DNS possui papel fundamental no funcionamento do Active Directory.

Por isso, o cliente foi configurado para utilizar o endereço IP do `DC01` como servidor DNS:

```text id="y6p1q9"
192.168.98.20
```

Dessa forma, o cliente consegue consultar os registros DNS utilizados para localizar serviços do domínio.

### Remote Desktop

O **Remote Desktop Protocol (RDP)** permite acessar remotamente uma máquina Windows.

Neste laboratório, o acesso remoto foi configurado para permitir que o usuário do domínio `nome1` se autenticasse no cliente.

### Autenticação de domínio

Ao utilizar uma conta do domínio, a autenticação passa a ser integrada à infraestrutura do Active Directory.

O fluxo simplificado utilizado na atividade foi:

```text id="c5v9x2"
Cliente Windows
      ↓
DNS → DC01
      ↓
Domínio aluno.hacker.com
      ↓
Autenticação do usuário
      ↓
Sessão RDP
```

---

## Resultado

O Windows Server 2022 cliente foi configurado para utilizar o `DC01` como servidor DNS e posteriormente associado ao domínio:

```text id="j8m4q6"
aluno.hacker.com
```

O usuário criado anteriormente no Active Directory foi configurado para acesso remoto e utilizado em uma nova conexão RDP.

A autenticação foi realizada utilizando a conta de domínio no Windows Server 2022 cliente.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 1 e 2**](../evidencias.pdf)

**Evidência registrada:** passo 10 — conexão RDP no Windows Server 2022 cliente utilizando o usuário do domínio.
