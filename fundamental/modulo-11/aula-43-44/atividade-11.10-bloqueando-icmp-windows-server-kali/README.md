# Atividade 11.10 — Bloqueando Pacotes ICMP Provenientes do Windows Server 2022 no Kali Linux

## Objetivo

Utilizar o **iptables** no Kali Linux para bloquear requisições **ICMP echo-request** provenientes do Windows Server 2022, verificando o efeito da regra através do comando `ping` e, posteriormente, removendo a regra para restaurar a comunicação.

---

## Ambiente

* **Kali Linux:** `192.168.98.40`
* **Windows Server 2022:** `192.168.98.30`
* **Ferramenta:** `iptables`
* **Protocolo:** ICMP
* **Tipo de ICMP bloqueado:** `echo-request`

---

## 1. Verificando o endereço IP do Windows Server 2022

O Windows Server 2022 foi acessado por RDP.

No Prompt de Comando, foi executado:

```cmd id="7h7udd"
ipconfig
```

A saída apresentada foi:

```text id="7h7udd"
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter Ethernet 2:

   Connection-specific DNS Suffix  . : ec2.internal
   Link-local IPv6 Address . . . . . : fe80::919a:6c84:9a17:42e3%7
   IPv4 Address. . . . . . . . . . . : 192.168.98.30
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.98.1
```

O endereço IPv4 do Windows Server utilizado no laboratório é:

```text id="q6m2vr"
192.168.98.30
```

---

## 2. Acessando o Kali Linux

A janela do RDP do Windows Server foi minimizada e o Kali Linux foi acessado através do endereço:

```text id="k8w4pn"
192.168.98.40
```

No Kali Linux, foi aberto o Terminal e obtido acesso administrativo com:

```bash id="p3r7xm"
sudo -i
```

---

## 3. Verificando as interfaces de rede do Kali

Foi executado:

```bash id="n5c9vk"
ifconfig
```

A interface `eth0` apresentou o endereço IPv4:

```text id="b1ocbt"
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
```

A interface `docker0` também estava presente:

```text id="r8m4qx"
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
```

A interface de loopback também estava disponível:

```text id="v7k2mp"
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1
```

O endereço utilizado pelo Kali na rede do laboratório é:

```text id="x4n8cq"
192.168.98.40
```

---

## 4. Testando a comunicação antes do bloqueio

No Windows Server 2022, foi executado:

```cmd id="m6p3wx"
ping 192.168.98.40
```

A comunicação funcionou normalmente:

```text id="yatahm"
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time=1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
```

Esse teste confirmou que, antes da aplicação da regra de firewall, o Windows Server conseguia enviar requisições ICMP para o Kali Linux e receber as respostas correspondentes.

O fluxo inicial era:

```text id="c8v5mz"
Windows Server
192.168.98.30
      │
      │ ICMP echo-request
      ▼
Kali Linux
192.168.98.40
      │
      │ ICMP echo-reply
      ▼
Windows Server
```

---

## 5. Criando a regra de bloqueio ICMP

No Kali Linux, foi criada a seguinte regra:

```bash id="h1refw"
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

A regra atua sobre os pacotes ICMP recebidos pelo Kali Linux.

### Parâmetros utilizados

#### `iptables`

Ferramenta utilizada para configurar regras de filtragem de pacotes através do Netfilter.

#### `-A INPUT`

Adiciona uma regra à chain `INPUT`.

A chain `INPUT` processa pacotes destinados ao próprio Kali Linux.

#### `-p icmp`

Define que a regra será aplicada ao protocolo:

```text id="w4n7cz"
ICMP
```

#### `--icmp-type echo-request`

Especifica o tipo de mensagem ICMP que será bloqueado:

```text id="s9m2vk"
echo-request
```

Esse é o tipo de mensagem utilizado pelo `ping` para solicitar uma resposta do host de destino.

#### `-j DROP`

Define a ação aplicada aos pacotes correspondentes.

`DROP` descarta o pacote, impedindo que ele seja processado normalmente pelo sistema.

Portanto, a regra pode ser interpretada como:

```text id="q5r8xm"
Pacote recebido
      ↓
      ICMP
      ↓
echo-request?
      ↓
     SIM
      ↓
     DROP
      ↓
Pacote descartado
```

> **Importante:** essa regra não bloqueia todo o protocolo ICMP. Ela corresponde especificamente a mensagens `echo-request`.

---

## 6. Testando o bloqueio

Após a criação da regra, o Windows Server 2022 foi utilizado novamente para executar:

```cmd id="d9k4vp"
ping 192.168.98.40
```

As requisições não receberam mais respostas do Kali Linux.

O resultado observado foi:

```text id="rsx7j0"
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.98.40:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

O `100% loss` demonstra que as quatro requisições enviadas pelo Windows Server não receberam respostas.

Isso ocorreu porque os pacotes `ICMP echo-request` foram descartados pelo `iptables` no Kali Linux.

### Evidência — Passo 10

**Frase obrigatória antes do print:**

> **Print da atividade 11.10:** resultado do `ping 192.168.98.40` executado no Windows Server 2022 após a aplicação da regra `iptables`, mostrando `100% loss` e ausência de respostas do Kali Linux.

[**Evidências — Módulo 11 / Aulas 43 e 44**](../evidencias.pdf)

---

## 7. Removendo a regra de bloqueio

Após confirmar o funcionamento do bloqueio, a regra foi removida no Kali Linux com:

```bash id="x7c3mp"
iptables -D INPUT -p icmp --icmp-type echo-request -j DROP
```

O parâmetro:

```text id="f2n8vk"
-D
```

remove uma regra existente.

Os demais parâmetros correspondem à regra que havia sido criada anteriormente.

---

## 8. Confirmando a comunicação novamente

Após remover a regra, o comando foi executado novamente no Windows Server:

```cmd id="j4p9wx"
ping 192.168.98.40
```

A comunicação voltou a funcionar:

```text id="xpiov4"
C:\Users\Administrator>ping 192.168.98.40

Pinging 192.168.98.40 with 32 bytes of data:
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time=1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64
Reply from 192.168.98.40: bytes=32 time<1ms TTL=64

Ping statistics for 192.168.98.40:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

O resultado mostra:

```text id="v6k2mq"
Packets: Sent = 4
Received = 4
Lost = 0 (0% loss)
```

Assim, após a remoção da regra, as requisições ICMP voltaram a receber respostas normalmente.

---

## 9. Encerrando a atividade

Após confirmar o funcionamento da comunicação, as janelas utilizadas durante o laboratório foram fechadas.

---

## Conceitos

* **ICMP:** protocolo utilizado para mensagens de controle e diagnóstico em redes IP.
* **Echo Request:** mensagem ICMP utilizada pelo `ping` para solicitar uma resposta.
* **Echo Reply:** resposta correspondente ao `echo-request`.
* **iptables:** ferramenta utilizada para configurar regras do Netfilter.
* **INPUT:** chain responsável pelo processamento de pacotes destinados ao próprio sistema.
* **DROP:** ação que descarta os pacotes correspondentes à regra.
* **Ping:** ferramenta utilizada para testar a conectividade através de mensagens ICMP.

## Fluxo da atividade

```text id="m8q3zr"
Windows Server
192.168.98.30
      ↓
ping 192.168.98.40
      ↓
Kali responde
      ↓
Criar regra ICMP DROP
      ↓
ping novamente
      ↓
100% loss
      ↓
Remover regra
      ↓
ping novamente
      ↓
0% loss
```

## Resultado

Foi criada uma regra `iptables` para descartar **ICMP echo-request** recebidos pelo Kali Linux. Após a aplicação da regra, o Windows Server apresentou `100% loss` ao executar `ping` contra `192.168.98.40`. A regra foi removida posteriormente e a comunicação foi restaurada, apresentando `0% loss`.
