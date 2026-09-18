# Atividade 3.4 — Netcat

## Objetivo

Utilizar o **Netcat (`nc`)** para criar um listener TCP em uma porta específica e observar uma requisição HTTP enviada pelo navegador.

A atividade demonstra, de forma prática, como uma ferramenta simples de rede pode receber conexões TCP e permitir a visualização dos dados transmitidos pelo cliente.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Netcat
* **Navegador:** Mozilla Firefox
* **Interface de rede:** `eth0`
* **IP da máquina Kali:** `192.168.98.40`
* **Porta utilizada:** `5555`
* **Protocolo observado:** HTTP

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Verificação da ajuda do Netcat

Foi utilizado o comando:

```bash
nc -help
```

O objetivo foi consultar as opções disponíveis na versão instalada do Netcat.

Saída observada:

```text
OpenBSD netcat (Debian patchlevel 1.229-1)
usage: nc [-46CDdFhklNnrStUuvZz] [-I length] [-i interval] [-M ttl]
          [-m minttl] [-O length] [-P proxy_username] [-p source_port]
          [-q seconds] [-s sourceaddr] [-T toskeyword] [-V rtable]
          [-w timeout] [-X proxy_protocol] [-x proxy_address[:port]]
          [destination] [port]

Command Summary:
-4              Use IPv4
-6              Use IPv6
-C              Send CRLF as line-ending
-D              Enable debugging
-d              Detach from stdin
-F              Pass socket fd
-h              Display this help text
-k              Keep inbound sockets open for multiple connections
-l              Listen for inbound rather than outbound connections
-N              Shutdown the network socket after EOF on stdin
-n              Suppress name/port resolutions
-r              Randomize remote ports
-S              Enable the TCP MD5 signature option
-s sourceaddr   Local source address
-t              Answer TELNET negotiation
-U              Use UNIX domain socket
-u              UDP mode
-v              Verbose
-w timeout      Timeout for connects and final net reads
-X proxy_protocol
-x proxy_address[:port]
-z              Zero-I/O mode
```

Entre as opções relevantes para a atividade estão:

* `-l` — coloca o Netcat em modo de escuta;
* `-p` — define a porta local utilizada;
* `-v` — habilita informações detalhadas sobre a conexão.

---

## 3. Identificação do endereço IP

Foi executado:

```bash
ifconfig
```

A interface utilizada no laboratório foi a `eth0`, configurada com o endereço:

```text
192.168.98.40
```

A interface estava associada à rede:

```text
192.168.98.0/24
```

Esse endereço foi utilizado posteriormente para acessar o listener através do Firefox.

---

## 4. Criação do listener

Foi iniciado um listener TCP na porta `5555`:

```bash
nc -l -p 5555 -v
```

O Netcat apresentou:

```text
listening on [any] 5555 ...
```

Nesse momento, o Netcat permaneceu aguardando uma conexão de entrada na porta `5555`.

A combinação utilizada pode ser entendida como:

```text
-l  → escutar conexões
-p  → utilizar a porta especificada
-v  → exibir informações detalhadas
```

---

## 5. Acesso pelo navegador

Com o listener ativo, foi aberto o Firefox e acessado:

```text
http://192.168.98.40:5555
```

O navegador tentou estabelecer uma conexão TCP com a porta `5555` da máquina Kali.

Como o Netcat estava escutando nessa porta, a conexão foi recebida pelo processo.

O navegador então enviou uma requisição HTTP ao listener.

---

## 6. Observação da requisição HTTP

A saída observada no terminal do Netcat foi:

```text
┌──(root㉿kali)-[~]
└─# nc -l -p 5555 -v
Listening on 0.0.0.0 5555
Connection received on ip-192-168-98-40.ec2.internal 42396
GET / HTTP/1.1
Host: 192.168.98.40:5555
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```

Esse foi o resultado principal observado na atividade.

O Netcat recebeu a conexão e exibiu diretamente no terminal os dados enviados pelo navegador.

### Interpretação da requisição

A primeira linha:

```text
GET / HTTP/1.1
```

indica uma requisição HTTP utilizando o método **GET** para solicitar o recurso `/`.

O campo:

```text
Host: 192.168.98.40:5555
```

identifica o destino da requisição, incluindo a porta utilizada.

O:

```text
User-Agent:
```

informa características do cliente HTTP. Nesse caso, a requisição foi realizada pelo Firefox executando em Linux.

O campo:

```text
Accept:
```

indica quais tipos de conteúdo o navegador aceita como resposta.

Já:

```text
Accept-Language: en-US,en;q=0.5
```

indica as preferências de idioma enviadas pelo navegador.

O:

```text
Accept-Encoding: gzip, deflate
```

informa mecanismos de compressão que o cliente aceita.

Por fim:

```text
Connection: keep-alive
```

indica a preferência do cliente por manter a conexão TCP aberta para outras comunicações.

---

## Conceitos praticados

### Netcat

O **Netcat** é uma ferramenta de rede utilizada para estabelecer conexões TCP/UDP, criar listeners e realizar testes de comunicação.

### Listener

Um listener é um processo que permanece aguardando conexões de entrada em determinado endereço e porta.

Neste laboratório:

```text
IP: 192.168.98.40
Porta: 5555
```

### TCP

A conexão estabelecida pelo navegador com o Netcat utilizou TCP, permitindo que o processo recebesse os dados enviados pelo cliente.

### HTTP

A requisição observada foi uma comunicação HTTP, permitindo visualizar diretamente seus elementos no terminal.

### HTTP Headers

Os cabeçalhos observados demonstram que uma requisição HTTP contém informações adicionais além do método e do caminho solicitado.

Entre eles:

* `Host`
* `User-Agent`
* `Accept`
* `Accept-Language`
* `Accept-Encoding`
* `Connection`

---

## Resultado

A atividade demonstrou como o Netcat pode ser utilizado para criar um listener TCP e observar uma requisição HTTP de forma direta.

O navegador realizou uma conexão com:

```text
192.168.98.40:5555
```

e o Netcat recebeu e exibiu no terminal:

* a conexão de entrada;
* a porta de origem;
* o método HTTP;
* o caminho solicitado;
* o protocolo HTTP;
* os cabeçalhos enviados pelo navegador.

O exercício ajudou a relacionar **TCP, portas, listeners, conexões de rede e estrutura de requisições HTTP**.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 9 e 10**](../evidencias.pdf)

**Print registrado:** etapa 6 da atividade, conforme solicitado pelo roteiro.
