# Atividade 3.7 — Criando um Honeypot com PentBox no Kali Linux

## Objetivo

Configurar um **honeypot** utilizando o PentBox no Kali Linux e realizar um teste controlado a partir de um Windows Server 2022.

A atividade demonstra como um honeypot pode simular um serviço acessível na rede e registrar uma tentativa de acesso, permitindo observar informações da conexão e da requisição HTTP.

> **Observação:** todo o procedimento foi realizado em ambiente de laboratório, exclusivamente para fins acadêmicos.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** PentBox 1.8
* **Sistema cliente:** Windows Server 2022
* **IP do Kali Linux:** `192.168.98.40`
* **Porta do honeypot:** `80`
* **Ferramenta de acesso:** Microsoft Edge

---

## 1. Acesso como superusuário

No Kali Linux, foi aberto o Terminal e executado:

```bash
sudo -i
```

Após a autenticação, o terminal passou a operar como `root`.

---

## 2. Verificação do endereço IP

Foi utilizado o comando:

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
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Loopback Local)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0
```

A interface utilizada para a comunicação com o restante do laboratório foi a `eth0`, configurada com o endereço:

```text
192.168.98.40
```

---

## 3. Acesso ao PentBox

Foi acessado o diretório do PentBox:

```bash
cd /curso/pentbox/pentbox-1.8
```

Em seguida, o programa foi executado:

```bash
./pentbox.rb
```

O menu principal apresentado foi:

```text
PenTBox 1.8 
         __
        U00U|.'@@@@@@`.
        |__|(@@@@@@@@@@)
             (@@@@@@@@)
             `YY~~~~YY'
              ||    ||

--------- Menu          ruby3.1.2 @ x86_64-linux-gnu

1- Cryptography tools

2- Network tools

3- Web

4- Ip grabber

5- Geolocation ip

6- Mass attack

7- License and contact

8- Exit

   ->
```

O PentBox reúne diferentes ferramentas, incluindo recursos relacionados a redes.

---

## 4. Seleção das ferramentas de rede

No menu principal, foi selecionada a opção:

```text
2- Network tools
```

O submenu apresentado foi:

```text
1- Net DoS Tester
2- TCP port scanner
3- Honeypot
4- Fuzzer
5- DNS and host gathering
6- MAC address geolocation (samy.pl)

0- Back
```

A opção `3` foi utilizada para acessar o recurso de honeypot.

---

## 5. Seleção do Honeypot

Foi selecionada:

```text
3- Honeypot
```

O PentBox apresentou:

```text
// Honeypot //

You must run PenTBox with root privileges.
                                                                                   
 Select option.

1- Fast Auto Configuration
2- Manual Configuration [Advanced Users, more options]
```

Foi escolhida a configuração automática:

```text
1- Fast Auto Configuration
```

---

## 6. Ativação do Honeypot

Após a seleção, o PentBox informou:

```text
HONEYPOT ACTIVATED ON PORT 80 (2024-01-24 16:52:52 -0500)
```

O honeypot passou a aguardar conexões na porta TCP `80`.

A porta `80` é tradicionalmente utilizada por serviços HTTP, o que permite que uma tentativa de acesso utilizando um navegador gere uma requisição HTTP observável pelo honeypot.

---

## 7. Teste a partir do Windows Server 2022

Com o honeypot ativo, foi acessado o Windows Server 2022 disponibilizado pelo laboratório.

No Windows, foi aberto o Microsoft Edge e inserido o endereço IP do Kali Linux:

```text
http://192.168.98.40
```

O acesso apresentou uma resposta indicando que a tentativa havia sido registrada pelo honeypot:

```text
Access denied
HTTP Referrer login failed
IP Address login failed
2025-09-06 11:44:50 -0300
```

A data e o horário exibidos podem variar conforme o momento em que o laboratório é executado.

---

## 8. Registro da tentativa de acesso pelo Honeypot

Após realizar o acesso pelo Windows Server, foi retornado ao Terminal do Kali Linux.

O PentBox registrou a tentativa de conexão:

```text
INTRUSION ATTEMPT DETECTED! from 192.168.98.30:49736 (2025-09-06 11:45:58 -0300)
-----------------------------
GET / HTTP/1.1
Host: 192.168.98.40
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36 Edg/139.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
```

Esse registro demonstra algumas informações importantes da requisição HTTP.

### Origem da conexão

```text
from 192.168.98.30:49736
```

Indica o endereço IP e a porta de origem observados pelo honeypot.

### Método HTTP

```text
GET / HTTP/1.1
```

Indica que o navegador realizou uma requisição HTTP `GET` para o caminho `/`.

### Host

```text
Host: 192.168.98.40
```

Identifica o endereço de destino utilizado na requisição HTTP.

### User-Agent

```text
User-Agent: Mozilla/5.0 (...) Edg/139.0.0.0
```

O campo `User-Agent` fornece informações sobre o cliente que realizou a requisição. Nesse caso, o registro identifica um navegador baseado em Chromium/Microsoft Edge executando em Windows.

### Accept

O campo `Accept` informa quais tipos de conteúdo o cliente declara ser capaz de receber.

### Accept-Encoding

```text
Accept-Encoding: gzip, deflate
```

Indica os métodos de compressão de conteúdo aceitos pelo cliente.

### Accept-Language

```text
Accept-Language: en-US,en;q=0.9
```

Indica as preferências de idioma enviadas pelo navegador.

---

## 9. Interpretação

O procedimento demonstra o funcionamento básico de um **honeypot**, que pode ser utilizado para apresentar um serviço aparentemente disponível e registrar interações com ele.

Nesse laboratório:

```text
Windows Server 2022
        │
        │ HTTP
        ▼
192.168.98.40:80
        │
        ▼
PentBox Honeypot
        │
        ▼
Registro da requisição
```

O PentBox identificou a tentativa de acesso e apresentou informações da requisição HTTP no terminal.

O registro permite observar dados como:

* endereço IP de origem;
* porta de origem;
* método HTTP;
* caminho solicitado;
* endereço de destino;
* navegador utilizado;
* sistema operacional informado pelo User-Agent;
* tipos de conteúdo aceitos;
* métodos de compressão aceitos;
* idioma informado pelo cliente.

---

## Conceitos praticados

### Honeypot

Um honeypot é um recurso criado para atrair, observar e registrar interações com atividades que não deveriam ocorrer em determinado serviço ou ambiente.

Em contextos de segurança, registros desse tipo podem auxiliar na detecção e análise de comportamentos suspeitos.

### PentBox

O PentBox é um conjunto de ferramentas voltadas para atividades de segurança e testes em redes. Nesta atividade, foi utilizado especificamente o módulo de honeypot.

### HTTP

O protocolo HTTP é utilizado para comunicação entre clientes, como navegadores, e servidores web.

A atividade permitiu observar diretamente uma requisição HTTP gerada pelo navegador.

### Logs e indicadores

A saída registrada pelo PentBox demonstra como informações de uma conexão podem ser utilizadas como evidência para análise de eventos de rede.

---

## Resultado

O honeypot foi configurado com sucesso no Kali Linux utilizando o PentBox e colocado em escuta na porta `80`.

A partir do Windows Server 2022, foi realizada uma requisição HTTP para o endereço do Kali Linux. O PentBox identificou a interação e registrou a requisição no terminal.

A atividade permitiu praticar:

1. configuração de um honeypot;
2. utilização de um serviço de escuta em uma porta TCP;
3. geração de uma requisição HTTP a partir de outro sistema;
4. identificação da origem da conexão;
5. análise de cabeçalhos HTTP;
6. observação de informações fornecidas pelo navegador.

---
## Evidência

[**Evidências — Módulo 3 / Aulas 11 e 12**](../evidencias.pdf)

**Print registrado:** etapa 10 da atividade, mostrando no terminal do Kali Linux a tentativa de acesso registrada pelo honeypot.
