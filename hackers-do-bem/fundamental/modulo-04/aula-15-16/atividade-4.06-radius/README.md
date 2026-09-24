# Atividade 4.6 — Implementando um servidor RADIUS no Kali Linux

## Objetivo

Implementar e testar um servidor **RADIUS (Remote Authentication Dial-In User Service)** utilizando o **FreeRADIUS** no Kali Linux.

A atividade demonstra um cenário de autenticação centralizada, no qual um cliente envia uma solicitação de autenticação para o servidor RADIUS. Foram realizados testes com um usuário previamente configurado e também com um usuário inexistente, permitindo observar tanto uma autenticação aceita quanto uma tentativa rejeitada.

O laboratório foi realizado em ambiente acadêmico controlado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Servidor RADIUS:** FreeRADIUS 3.2.3
* **Interface de rede:** `eth0`
* **IP do laboratório:** `192.168.98.40`
* **Loopback:** `127.0.0.1`
* **Porta RADIUS de autenticação:** `1812`
* **Porta RADIUS de contabilidade:** `1813`
* **Ferramenta de teste:** `radtest`

> As credenciais utilizadas para acesso à VM do curso não são registradas neste README.

---

## 1. Acesso administrativo

Inicialmente, foi aberto o terminal e obtido acesso de superusuário:

```bash
sudo -i
```

A senha utilizada para elevação de privilégio pertence ao ambiente do laboratório e não é reproduzida neste documento.

---

## 2. Verificação das interfaces de rede

Foi utilizado o comando `ifconfig` para verificar as interfaces disponíveis, principalmente a interface de loopback:

```bash
ifconfig
```

Saída observada:

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:df:26:13:80  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::1005:27ff:fe44:1631  prefixlen 64  scopeid 0x20<link>
        ether 12:05:27:44:16:31  txqueuelen 1000  (Ethernet)
        RX packets 1818194  bytes 2694820836 (2.5 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61082  bytes 77348531 (73.7 MiB)
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Ethernet)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
```

As interfaces principais observadas foram:

* `docker0` — interface relacionada à rede Docker;
* `eth0` — interface de rede utilizada pela VM, com endereço `192.168.98.40`;
* `lo` — interface de loopback, utilizando `127.0.0.1`.

A atividade utiliza a interface de loopback para realizar os testes locais de autenticação.

---

## 3. Verificação dos arquivos do FreeRADIUS

Os arquivos de configuração do FreeRADIUS foram listados com:

```bash
ls /etc/freeradius/3.0
```

Saída:

```text
certs         experimental.conf  mods-available  panic.gdb
clients.conf  hints              mods-config      policy.d
dictionary    huntgroups         mods-enabled     proxy.conf
README.rst    radiusd.conf       sites-enabled    templates.conf
sites-available  trigger.conf    users
```

O diretório contém os principais arquivos e diretórios utilizados pelo FreeRADIUS, incluindo:

* `clients.conf` — configuração dos clientes RADIUS;
* `users` — arquivo utilizado no laboratório para definir o usuário de teste;
* `sites-enabled` — configurações dos servidores virtuais habilitados;
* `mods-enabled` — módulos habilitados;
* `radiusd.conf` — configuração principal do serviço.

---

## 4. Verificação dos clientes RADIUS

Foi consultado o arquivo de configuração dos clientes:

```bash
cat /etc/freeradius/3.0/clients.conf
```

No ambiente do laboratório, havia um cliente localhost previamente configurado.

A configuração relevante apresentada pelo roteiro utiliza:

```text
#  The default secret below is only for testing, and should
#  not be used in any real environment.
#
secret = testing123
```

O valor `testing123` é uma **shared secret** utilizada pelo cliente e pelo servidor para proteger e validar a comunicação RADIUS no cenário de teste.

> Essa configuração é apropriada apenas para o laboratório. Uma shared secret previsível não deve ser utilizada em um ambiente de produção.

---

## 5. Criação do usuário de teste

Foi editado o arquivo de usuários do FreeRADIUS:

```bash
nano /etc/freeradius/3.0/users
```

A entrada adicionada foi:

```text
usuario1 Cleartext-Password := "[senha definida no laboratório]"
```

O usuário `usuario1` foi utilizado posteriormente para testar uma autenticação válida.

A senha original utilizada durante o laboratório não é publicada neste README.

Após a edição, o arquivo foi salvo utilizando:

```text
Ctrl + X
S
ENTER
```

---

## 6. Inicialização do FreeRADIUS

O servidor foi iniciado em modo de depuração com:

```bash
freeradius -X
```

O modo `-X` é particularmente útil em laboratório porque apresenta no terminal o processamento detalhado das requisições recebidas.

Saída inicial:

```text
FreeRADIUS Version 3.2.3
Copyright (C) 1999-2022 The FreeRADIUS server project and contributors
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE
You may redistribute copies of the software under the terms of the
GNU General Public License
For more information about these matters, see the file named COPYRIGHT
Starting - reading configuration files ...
including dictionary file /usr/share/freeradius/dictionary
including dictionary file /usr/share/freeradius/dictionary.dhcp

...

listen {
        type = "acct"
        ipv6addr = ::
        port = 0
   limit {
        max_connections = 16
        lifetime = 0
        idle_timeout = 30
   }
}
listen {
        type = "auth"
        ipaddr = 127.0.0.1
        port = 18120
}
Listening on auth address * port 1812 bound to server default
Listening on acct address * port 1813 bound to server default
Listening on auth address :: port 1812 bound to server default
Listening on acct address :: port 1813 bound to server default
Listening on auth address 127.0.0.1 port 18120 bound to server inner-tunnel
Listening on proxy address * port 43055
Listening on proxy address :: port 36998
Ready to process requests
```

A mensagem:

```text
Ready to process requests
```

indica que o FreeRADIUS terminou o carregamento da configuração e está pronto para receber requisições.

No cenário observado:

* `1812` — autenticação RADIUS;
* `1813` — contabilidade RADIUS;
* `127.0.0.1:18120` — servidor `inner-tunnel`.

---

## 7. Teste de autenticação com usuário válido

Em um segundo terminal, foi realizado um teste utilizando o `radtest`:

```bash
radtest usuario1 [senha-do-laboratório] 127.0.0.1 0 testing123
```

A saída observada foi:

```text
Sent Access-Request Id 246 from 0.0.0.0:af56 to 127.0.0.1:1812 length 78
        User-Name = "usuario1"
        User-Password = "[senha-do-laboratório]"
        NAS-IP-Address = 127.0.1.1
        NAS-Port = 0
        Message-Authenticator = 0x00
        Cleartext-Password = "[senha-do-laboratório]"
Received Access-Accept Id 246 from 127.0.0.1:714 to 127.0.0.1:44886 length 20
Message-Authenticator = 0xca5dfd87ba2b797e16edfe5c7ecb1d40
```

O resultado mais importante é:

```text
Received Access-Accept
```

Isso indica que o servidor RADIUS aceitou a solicitação de autenticação.

### Parâmetros utilizados

| Parâmetro    | Função                                                   |
| ------------ | -------------------------------------------------------- |
| `radtest`    | Ferramenta utilizada para testar uma autenticação RADIUS |
| `usuario1`   | Usuário configurado no FreeRADIUS                        |
| senha        | Credencial definida para o usuário no laboratório        |
| `127.0.0.1`  | Endereço do servidor RADIUS utilizado no teste           |
| `0`          | NAS-Port utilizado pela ferramenta no teste              |
| `testing123` | Shared secret configurada para o cliente de teste        |

---

## 8. Análise do log da autenticação aceita

No primeiro terminal, o FreeRADIUS registrou o processamento da requisição.

Trechos principais:

```text
Ready to process requests
(0)     Received Access-Request Id 246 from 127.0.0.1:40968 to 127.0.0.1:1812 length 78
(0)   Message-Authenticator = 0x80ae90efd30a3e6e0d4f9cac1c5a16b6
(0)   User-Name = "usuario1"
(0)   User-Password = "[senha-do-laboratório]"
(0)   NAS-IP-Address = 127.0.1.1
(0)   NAS-Port = 0
(0) # Executing section authorize from file /etc/freeradius/3.0/sites-enabled/default
(0)   authorize {
(0)     policy filter_username {
(0)       if (&User-Name) {
(0)       if (&User-Name)  -> TRUE
(0)       if (&User-Name)  {
(0)         if (&User-Name =~ / /) {
(0)         if (&User-Name =~ / /)  -> FALSE
(0)         if (&User-Name =~ /@[^@]*@/ ) {
(0)         if (&User-Name =~ /@[^@]*@/ )  -> FALSE
(0)         if (&User-Name =~ /\.\./ ) {
(0)         if (&User-Name =~ /\.\./ )  -> FALSE
(0)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))  {
(0)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))   -> FALSE
(0)         if (&User-Name =~ /\.$/)  {
(0)         if (&User-Name =~ /\.$/)   -> FALSE
(0)         if (&User-Name =~ /@\./)  {
(0)         if (&User-Name =~ /@\./)   -> FALSE
(0)       } # if (&User-Name)  = notfound
(0)     } # policy filter_username = notfound
(0)     [preprocess] = ok
(0)     [chap] = noop
(0)     [mschap] = noop
(0)     [digest] = noop
(0) suffix: Checking for suffix after "@"
(0) suffix: No '@' in User-Name = "usuario1", looking up realm NULL
(0) suffix: No such realm "NULL"
(0)     [suffix] = noop
(0) eap: No EAP-Message, not doing EAP
(0)     [eap] = noop
(0) files: users: Matched entry usuario1 at line 91
(0)     [files] = ok
(0)     [expiration] = noop
(0)     [logintime] = noop
(0)     [pap] = updated
(0)   } # authorize = updated
(0) Found Auth-Type = PAP
(0) # Executing group from file /etc/freeradius/3.0/sites-enabled/default
(0)   Auth-Type PAP {
(0)     pap: Login attempt with password
(0)     pap: Comparing with "known good" Cleartext-Password
(0)     pap: User authenticated successfully
(0)     [pap] = ok
(0)   } # Auth-Type PAP = ok
(0) # Executing section post-auth from file /etc/freeradius/3.0/sites-enabled/default
(0)   post-auth {
(0)     if (session-state:User-Name && reply:User-Name && request:User-Name && (reply:User-Name == request:User-Name)) {
(0)     if (session-state:User-Name && reply:User-Name && request:User-Name && (reply:User-Name == request:User-Name))  -> FALSE
(0)     update {
(0)       No attributes updated for RHS &session-state:
(0)     } # update = noop
(0)     [exec] = noop
(0)     policy remove_reply_message_if_eap {
(0)       if (&reply:EAP-Message && &reply:Reply-Message) {
(0)       if (&reply:EAP-Message && &reply:Reply-Message)  -> FALSE
(0)       else {
(0)         [noop] = noop
(0)       } # else = noop
(0)     } # policy remove_reply_message_if_eap = noop
(0)     if (EAP-Key-Name && &reply:EAP-Session-Id) {
(0)     if (EAP-Key-Name && &reply:EAP-Session-Id)  -> FALSE
(0)   } # post-auth = noop
(0) Sent Access-Accept Id 246 from 127.0.0.1:1812 to 127.0.0.1:44886 length 20
(0) Finished request
Waking up in 4.9 seconds.
(0) Cleaning up request packet ID 246 with timestamp +69 due to cleanup_delay was reached
Ready to process requests
```

### Interpretação

O fluxo observado foi:

1. O FreeRADIUS recebeu um `Access-Request`.
2. O usuário `usuario1` foi localizado no arquivo `users`.
3. A entrada do usuário foi considerada válida pela seção `files`.
4. O servidor definiu `Auth-Type = PAP`.
5. O módulo PAP comparou a senha apresentada com a credencial configurada.
6. A autenticação foi concluída com sucesso.
7. O servidor enviou `Access-Accept`.

A linha mais significativa é:

```text
pap: User authenticated successfully
```

seguida por:

```text
Sent Access-Accept
```

---

## 9. Teste com usuário inexistente

Depois do teste bem-sucedido, foi realizada uma nova tentativa utilizando um usuário que não estava configurado:

```bash
radtest usuarioX [senha-do-laboratório] 127.0.0.1 0 testing123
```

Saída:

```text
Sent Access-Request Id 211 from 0.0.0.0:bd19 to 127.0.0.1:1812 length 78
        User-Name = "usuarioX"
        User-Password = "[senha-do-laboratório]"
        NAS-IP-Address = 127.0.1.1
        NAS-Port = 0
        Message-Authenticator = 0x00
        Cleartext-Password = "[senha-do-laboratório]"
Received Access-Reject Id 211 from 127.0.0.1:714 to 127.0.0.1:60653 length 20
        Message-Authenticator = 0xf9a00ead8e578adcede7fa8190a3bffb
(0) -: Expected Access-Accept got Access-Reject
```

O resultado foi diferente do teste anterior:

```text
Received Access-Reject
```

Isso demonstra que a autenticação do usuário inexistente foi rejeitada.

---

## 10. Análise do log da autenticação rejeitada

O primeiro terminal registrou o processamento da tentativa:

```text
Ready to process requests
(1) Received Access-Request Id 211 from 127.0.0.1:60653 to 127.0.0.1:1812 length 78
(1)   Message-Authenticator = 0x82d0c1a625c7db2b6d59b94efb8b37ba
(1)   User-Name = "usuarioX"
(1)   User-Password = "[senha-do-laboratório]"
(1)   NAS-IP-Address = 127.0.1.1
(1)   NAS-Port = 0
(1) # Executing section authorize from file /etc/freeradius/3.0/sites-enabled/default
(1)   authorize {
(1)     policy filter_username {
(1)       if (&User-Name) {
(1)       if (&User-Name)  -> TRUE
(1)       if (&User-Name)  {
(1)         if (&User-Name =~ / /) {
(1)         if (&User-Name =~ / /)  -> FALSE
(1)         if (&User-Name =~ /@[^@]*@/ ) {
(1)         if (&User-Name =~ /@[^@]*@/ )  -> FALSE
(1)         if (&User-Name =~ /\.\./ ) {
(1)         if (&User-Name =~ /\.\./ )  -> FALSE
(1)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))  {
(1)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))   -> FALSE
(1)         if (&User-Name =~ /\.$/)  {
(1)         if (&User-Name =~ /\.$/)   -> FALSE
(1)         if (&User-Name =~ /@\./)  {
(1)         if (&User-Name =~ /@\./)   -> FALSE
(1)       } # if (&User-Name)  = notfound
(1)     } # policy filter_username = notfound
(1)     [preprocess] = ok
(1)     [chap] = noop
(1)     [mschap] = noop
(1)     [digest] = noop
(1) suffix: Checking for suffix after "@"
(1) suffix: No '@' in User-Name = "usuarioX", looking up realm NULL
(1) suffix: No such realm "NULL"
(1)     [suffix] = noop
(1) eap: No EAP-Message, not doing EAP
(1)     [eap] = noop
(1)     [files] = noop
(1)     [expiration] = noop
(1)     [logintime] = noop
(1) pap: WARNING: No "known good" password found for the user.  Not setting Auth-Type
(1) pap: WARNING: Authentication will fail unless a "known good" password is available
(1)     [pap] = noop
(1)   } # authorize = ok
(1) ERROR: No Auth-Type found: rejecting the user via Post-Auth-Type = Reject
(1) Failed to authenticate the user
(1) Using Post-Auth-Type Reject
(1) # Executing group from file /etc/freeradius/3.0/sites-enabled/default
(1)   Post-Auth-Type REJECT {
(1)     attr_filter.access_reject: EXPAND %{User-Name}
(1)     attr_filter.access_reject:    --> usuarioX
(1)     attr_filter.access_reject: Matched entry DEFAULT at line 11
(1)     [attr_filter.access_reject] = updated
(1)     [eap] = noop
(1)     policy remove_reply_message_if_eap {
(1)       if (&reply:EAP-Message && &reply:Reply-Message) {
(1)       if (&reply:EAP-Message && &reply:Reply-Message)  -> FALSE
(1)       else {
(1)         [noop] = noop
(1)       } # else = noop
(1)     } # policy remove_reply_message_if_eap = noop
(1)   } # Post-Auth-Type REJECT = updated
(1) Delaying response for 1.000000 seconds
Waking up in 0.3 seconds.
Waking up in 0.6 seconds.
(1) Sending delayed response
(1) Sent Access-Reject Id 211 from 127.0.0.1:1812 to 127.0.0.1:60653 length 20
Waking up in 3.9 seconds.
(1) Cleaning up request packet ID 211 with timestamp +412 due to cleanup_delay was reached
Ready to process requests
```

### Interpretação

Diferentemente do usuário `usuario1`, a entrada de `usuarioX` não foi encontrada no arquivo de usuários.

O log evidencia isso por meio de:

```text
[files] = noop
```

e posteriormente:

```text
pap: WARNING: No "known good" password found for the user.
```

Como não havia uma credencial válida associada ao usuário, o servidor não definiu um `Auth-Type` para realizar a autenticação:

```text
ERROR: No Auth-Type found: rejecting the user via Post-Auth-Type = Reject
```

Por fim, o servidor enviou:

```text
Sent Access-Reject
```

Assim, o segundo teste demonstrou o comportamento do FreeRADIUS diante de uma tentativa de autenticação para um usuário não cadastrado.

---

## Conceitos praticados

### RADIUS

O **RADIUS** é um protocolo utilizado para autenticação, autorização e contabilidade em ambientes de rede.

### FreeRADIUS

O FreeRADIUS é uma implementação de código aberto do protocolo RADIUS e pode atuar como servidor centralizado de autenticação.

### Access-Request

Mensagem enviada pelo cliente ao servidor RADIUS solicitando a autenticação de um usuário.

### Access-Accept

Resposta utilizada quando o servidor aceita a solicitação de autenticação.

### Access-Reject

Resposta enviada quando a solicitação não pode ser autenticada.

### Shared Secret

Segredo compartilhado entre o cliente RADIUS e o servidor, utilizado como parte da proteção e validação da comunicação.

### PAP

O **Password Authentication Protocol** foi o método observado durante o teste do usuário configurado. O log apresentou:

```text
Found Auth-Type = PAP
```

e:

```text
pap: User authenticated successfully
```

---

## Resultado

A atividade permitiu implementar um servidor FreeRADIUS e validar seu funcionamento utilizando requisições locais.

Foram realizados dois cenários:

| Cenário                              | Resultado       |
| ------------------------------------ | --------------- |
| `usuario1` configurado no FreeRADIUS | `Access-Accept` |
| `usuarioX` não configurado           | `Access-Reject` |

O primeiro teste demonstrou o fluxo completo de uma autenticação aceita, enquanto o segundo mostrou como o servidor rejeita uma tentativa quando não encontra uma credencial válida para o usuário solicitado.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 3 e 4**](../evidencias.pdf)

**Print registrado:** etapa 11 da atividade, conforme solicitado pelo roteiro geral de evidências do Módulo 4.
